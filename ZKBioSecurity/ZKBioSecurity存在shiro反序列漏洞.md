# ZKBioSecurity存在shiro反序列漏洞

ZKBioSecurity平台存在 shiro 反序列化漏洞，该漏洞源于软件存在硬编码的 shiro-key，攻击者可利用该 key 生成恶意的序列化数据，在服务器上执行任意代码，执行系统命令、或打入内存马等，获取服务器权限。

## fofa

```javascript
title=="ZKBioSecurity" && body="Automatic login within two weeks"
```

## poc

利用工具

```
https://github.com/SummerSec/ShiroAttack2/releases/tag/4.7.0
```

![image-20241106225639218](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411062256286.png)